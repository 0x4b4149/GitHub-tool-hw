<template>
  <div class="container">
    <!-- 標題：有點像店的招牌 -->
    <h1>🔍 GitHub 偵察機</h1>
    
    <!-- 輸入框：讓你寫下要搜尋的名字 -->
    <!-- v-model 就像是把輸入的內容放進盒子裡 -->
    <input 
      v-model="名字盒子" 
      placeholder="請輸入 GitHub 帳號" 
    />
    
    <!-- 按鈕：按下後會觸發搜尋功能 -->
    <button @click="搜尋功能">搜尋</button>
    
    <!-- 顯示結果區域：找到後會顯示在這裡 -->
    <!-- v-if="照片盒子" 像開關：如果有照片就顯示結果 -->
    <!-- v-else 如果沒有照片（也就是查不到），就顯示這行字 -->
    <div v-if="照片盒子" class="result">
      <!-- 這裡會顯示找到的頭像 -->
      <img :src="照片盒子" alt="頭像" />
      <!-- 這裡會顯示用户名 -->
      <p>{{ 名字盒子 }}</p>
    </div>
    
    <!-- v-else：當上面那個不成立的時候（照片盒子是空的），顯示這行字 -->
    <div v-else-if="錯誤盒子" class="error">
      {{ 錯誤盒子 }}
    </div>
  </div>
</template>

<script>
// 引入 ref（像一個裝資料的盒子）
import { ref } from 'vue'

// 建立一個盒子叫做「名字盒子」，一開始是空的
const 名字盒子 = ref('')

// 建立一個盒子叫做「照片盒子」，一開始也是空的
const 照片盒子 = ref('')

// 建立一個盒子叫做「錯誤盒子」，用來放「查無此人」這行字
const 錯誤盒子 = ref('')

// 搜尋功能的工廠
function 搜尋功能() {
  // 每次搜尋前，先把錯誤盒子清空
  錯誤盒子.value = ''
  
  // 用 GitHub API 去抓資料
  fetch('https://api.github.com/users/' + 名字盒子.value)
    .then(response => {
      // 如果找不到這個人（HTTP 狀態不是 200）
      if (!response.ok) {
        // 把「查無此人」放進錯誤盒子
        錯誤盒子.value = '查無此人'
        // 把照片盒子清空
        照片盒子.value = ''
        // 結束這個工廠
        return
      }
      return response.json()
    })
    .then(data => {
      // 把找到的頭像網址放進照片盒子
      照片盒子.value = data.avatar_url
    })
}

// 把這些功能都傳給模板使用
export default {
  setup() {
    return {
      名字盒子,
      照片盒子,
      錯誤盒子,
      搜尋功能
    }
  }
}
</script>

<style>
/* 深色背景，就像晚上一樣 */
body {
  background-color: #1a1a2e;
  color: #ffffff;
  margin: 0;
  min-height: 100vh;
}

/* 讓畫面好看一點的化妝師（CSS） */
.container {
  text-align: center;
  padding: 50px;
  font-family: sans-serif;
}

input {
  padding: 10px;
  font-size: 16px;
  width: 200px;
  border-radius: 8px;
  border: 2px solid #444;
  background-color: #16213e;
  color: #fff;
}

button {
  padding: 10px 20px;
  font-size: 16px;
  margin-left: 10px;
  cursor: pointer;
  border-radius: 8px;
  background-color: #0f3460;
  color: #fff;
  border: none;
}

button:hover {
  background-color: #e94560;
}

.result {
  margin-top: 30px;
}

.result img {
  width: 150px;
  height: 150px;
  border-radius: 50%;
  border: 3px solid #e94560;
}

.error {
  margin-top: 30px;
  color: #e94560;
  font-size: 18px;
}
</style>