<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const hours = ref(34)
const minutes = ref(33)
const seconds = ref(47)

let timer = null

const updateCountdown = () => {
  if (seconds.value > 0) {
    seconds.value--
  } else {
    if (minutes.value > 0) {
      minutes.value--
      seconds.value = 59
    } else {
      if (hours.value > 0) {
        hours.value--
        minutes.value = 59
        seconds.value = 59
      }
    }
  }
}

const formatNumber = (num) => {
  return num.toString().padStart(2, '0')
}

onMounted(() => {
  timer = setInterval(updateCountdown, 1000)
})

onUnmounted(() => {
  if (timer) {
    clearInterval(timer)
  }
})
</script>

<template>
  <div class="coupon-banner">
    <div class="banner-left">
      <div class="gift-icon">
        <img class="gift-emoji" src="https://img.alicdn.com/imgextra/i2/O1CN01oy7beb1jAG3oaJjxG_!!6000000004507-2-tps-128-128.png" alt="gift" />
      </div>
      <span class="coupon-text">
        您有<strong>2张共计138元</strong>消费券，可尽快使用
      </span>
    </div>
    <div class="banner-right">
      <span class="countdown-label">距结束</span>
      <span class="countdown-box">{{ formatNumber(hours) }}</span>
      <span class="countdown-separator">:</span>
      <span class="countdown-box">{{ formatNumber(minutes) }}</span>
      <span class="countdown-separator">:</span>
      <span class="countdown-box countdown-seconds">{{ formatNumber(seconds) }}</span>
    </div>
  </div>
  <div class="divider"></div>
</template>

<style scoped>
.coupon-banner {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background: linear-gradient(90deg, #fff5f5 0%, #fff0f0 100%);
  border: 1px solid rgb(254, 23, 69);
  border-radius: 8px;
  padding: 12px 16px;
  margin-bottom: 16px;
}

.banner-left {
  display: flex;
  align-items: center;
  gap: 10px;
}

.gift-icon {
  display: flex;
  align-items: center;
  justify-content: center;
}

.gift-emoji {
  width: 32px;
  height: 32px;
  object-fit: contain;
}

.coupon-text {
  color: #fe1745;
  font-size: 14px;
  font-weight: 500;
  line-height: 22px;
  white-space: nowrap;
}

.coupon-text strong {
  color: #ff0036;
  padding: 0 2px;
  font-size: 20px;
  font-weight: bold;
}

.banner-right {
  display: flex;
  align-items: center;
  gap: 4px;
  font-size: 15px;
  color: #666;
}

.countdown-label {
  color: #fe1745;
  font-size: 14px;
  font-weight: 500;
  line-height: 22px;
  white-space: nowrap;
  margin-right: 6px;
}

.countdown-box {
  align-items: center;
  background-color: #fe1745;
  border-radius: 3px;
  color: #fff;
  display: flex;
  font-size: 12px;
  height: 16px;
  justify-content: center;
  min-width: 18px;
}

.countdown-separator {
  color: #ff4d4f;
  font-weight: normal;
  font-size: 15px;
}

.countdown-seconds {
  font-weight: normal;
}

.divider {
  border-bottom: 1px solid #f0f0f0;
  margin-bottom: 16px;
}
</style>