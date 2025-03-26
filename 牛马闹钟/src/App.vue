<template>
  <div class="container" data-tauri-drag-region>
    <div class="titlebar">
      <div class="titlebar-text">牛马时钟</div>
    </div>
    <div class="content">
      <div class="time">{{ time }}</div>
      <div class="date">{{ date }}</div>
      <div class="animal">{{ animal }}</div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue'

const time = ref('00:00:00')
const date = ref('2024年1月1日 星期一')
const animal = ref('🐮')

const updateClock = () => {
  const now = new Date()
  
  // 更新时间
  const hours = String(now.getHours()).padStart(2, '0')
  const minutes = String(now.getMinutes()).padStart(2, '0')
  const seconds = String(now.getSeconds()).padStart(2, '0')
  time.value = `${hours}:${minutes}:${seconds}`
  
  // 更新日期
  const year = now.getFullYear()
  const month = now.getMonth() + 1
  const day = now.getDate()
  const weekdays = ['星期日', '星期一', '星期二', '星期三', '星期四', '星期五', '星期六']
  const weekday = weekdays[now.getDay()]
  date.value = `${year}年${month}月${day}日 ${weekday}`
  
  // 切换牛马图标
  animal.value = now.getSeconds() % 2 === 0 ? '🐮' : '🐴'
}

onMounted(() => {
  updateClock()
  setInterval(updateClock, 1000)
})
</script>

<style scoped>
.container {
  text-align: center;
  background: rgba(255, 255, 255, 0.9);
  width: 300px;
  margin: 0;
  height: 100vh;
  display: flex;
  flex-direction: column;
}

.titlebar {
  height: 30px;
  background: #2c3e50;
  user-select: none;
  display: flex;
  align-items: center;
  padding: 0 10px;
  color: white;
  font-size: 14px;
}

.titlebar-text {
  margin-left: 8px;
}

.content {
  flex: 1;
  padding: 20px;
}

h1 {
  margin: 0 0 10px 0;
  font-size: 1.5rem;
  color: #333;
}

.time {
  font-size: 2.5rem;
  font-weight: bold;
  color: #2c3e50;
}

.date {
  font-size: 1.1rem;
  color: #666;
  margin: 10px 0;
}

.animal {
  font-size: 3.5rem;
  margin: 10px 0;
  animation: bounce 1s infinite alternate;
}

@keyframes bounce {
  from {
    transform: translateY(0);
  }
  to {
    transform: translateY(-10px);
  }
}
</style>
