<template>
  <div class="coupon-banner">
    <div class="banner-left">
      <span class="coupon-icon">🎁</span>
      <span class="coupon-text">您有 <strong>2张共计138元</strong> 消费券，可尽快使用</span>
    </div>
    <div class="banner-right">
      <span class="countdown">距结束 <strong>52:18:51</strong></span>
    </div>
  </div>
</template>

<style scoped>
.coupon-banner {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background: linear-gradient(90deg, #fff5f5 0%, #fff0f0 100%);
  border: 1px solid #ffcccc;
  border-radius: 4px;
  padding: 12px 16px;
  margin-bottom: 16px;
}

.banner-left {
  display: flex;
  align-items: center;
  gap: 8px;
}

.coupon-icon {
  font-size: 20px;
}

.coupon-text {
  font-size: 14px;
  color: #333;
}

.coupon-text strong {
  color: #ff5000;
  font-weight: bold;
}

.banner-right {
  font-size: 14px;
  color: #666;
}

.countdown strong {
  color: #ff5000;
  font-weight: bold;
  font-family: monospace;
}
</style>
