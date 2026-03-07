<script setup>
const props = defineProps({
  selectedCount: {
    type: Number,
    required: true
  },
  totalPrice: {
    type: String,
    required: true
  }
})
</script>

<template>
  <div class="right-sidebar">
    <div class="search-box">
      <div class="search-input-wrapper">
        <input type="text" class="search-input" placeholder="淡人高知穿搭一整套" />
        <span class="camera-icon">📷</span>
      </div>
      <button class="search-btn">搜淘宝</button>
    </div>

    <div class="checkout-box">
      <div class="checkout-title">结算明细</div>
      <div class="checkout-content">
        <div class="empty-cart" v-if="selectedCount === 0">
          <div class="empty-icon-wrapper">
            <div class="empty-icon">🛒</div>
            <span class="empty-badge">空</span>
          </div>
          <div class="empty-text">选择商品查看实际支付价格</div>
        </div>
        <div class="checkout-summary" v-else>
          <div class="summary-row">
            <span class="summary-label">合计：</span>
            <span class="summary-amount">¥{{ totalPrice }}</span>
          </div>
        </div>
      </div>
      <div class="total-row" v-if="selectedCount === 0">
        <span class="total-label">合计：</span>
        <span class="total-amount">¥ 0</span>
      </div>
      <button class="checkout-btn" :disabled="selectedCount === 0">结算</button>
    </div>
  </div>

  <div class="toolbar-icons">
    <div class="toolbar-icon" title="首页">🏠</div>
    <div class="toolbar-icon" title="消息">💬</div>
    <div class="toolbar-icon" title="购物车">🛒</div>
    <div class="toolbar-icon" title="我的订单">📋</div>
    <div class="toolbar-icon" title="我的收藏">❤️</div>
    <div class="toolbar-icon" title="历史浏览">📜</div>
    <div class="toolbar-icon" title="回到顶部">↑</div>
  </div>
</template>

<style scoped>
.right-sidebar {
  position: fixed;
  right: 56px;
  top: 0;
  bottom: 0;
  width: 280px;
  background-color: #fff;
  border-left: 1px solid #eee;
  padding: 20px;
  overflow-y: auto;
  z-index: 50;
}

.search-box {
  display: flex;
  gap: 8px;
  margin-bottom: 20px;
}

.search-input-wrapper {
  flex: 1;
  position: relative;
  display: flex;
  align-items: center;
}

.search-input {
  width: 100%;
  padding: 10px 36px 10px 12px;
  border: 1px solid #ddd;
  border-radius: 8px 0 0 8px;
  font-size: 14px;
  outline: none;
}

.search-input:focus {
  border-color: #ff5000;
}

.camera-icon {
  position: absolute;
  right: 10px;
  font-size: 18px;
  cursor: pointer;
}

.search-btn {
  background-color: #ff5000;
  color: white;
  border: none;
  padding: 10px 20px;
  border-radius: 0 8px 8px 0;
  font-size: 14px;
  font-weight: 500;
  cursor: pointer;
  white-space: nowrap;
}

.search-btn:hover {
  background-color: #ff4400;
}

.checkout-box {
  background-color: #fff;
  border: 1px solid #eee;
  border-radius: 12px;
  padding: 20px;
}

.checkout-title {
  font-size: 18px;
  font-weight: bold;
  color: #333;
  margin-bottom: 24px;
}

.checkout-content {
  min-height: 160px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.empty-cart {
  text-align: center;
}

.empty-icon-wrapper {
  position: relative;
  display: inline-block;
  margin-bottom: 16px;
}

.empty-icon {
  font-size: 72px;
  opacity: 0.3;
}

.empty-badge {
  position: absolute;
  top: 8px;
  right: -8px;
  background-color: #ff5000;
  color: white;
  font-size: 12px;
  padding: 2px 8px;
  border-radius: 12px;
}

.empty-text {
  font-size: 16px;
  color: #ff5000;
  font-weight: 500;
}

.checkout-summary {
  width: 100%;
  padding: 12px 0;
}

.summary-row {
  display: flex;
  justify-content: space-between;
  align-items: center;
  font-size: 14px;
}

.summary-label {
  color: #666;
}

.summary-amount {
  font-size: 20px;
  font-weight: bold;
  color: #ff5000;
}

.total-row {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 16px;
  padding-top: 16px;
  border-top: 1px solid #f5f5f5;
}

.total-label {
  font-size: 18px;
  font-weight: bold;
  color: #333;
}

.total-amount {
  font-size: 24px;
  font-weight: bold;
  color: #ff5000;
}

.checkout-btn {
  width: 100%;
  padding: 16px;
  background-color: #ff5000;
  color: white;
  border: none;
  border-radius: 12px;
  font-size: 18px;
  font-weight: bold;
  cursor: pointer;
  margin-top: 8px;
}

.checkout-btn:hover:not(:disabled) {
  background-color: #ff4400;
}

.checkout-btn:disabled {
  background-color: #ffb380;
  cursor: not-allowed;
}

.toolbar-icons {
  position: fixed;
  right: 0;
  top: 0;
  bottom: 0;
  width: 56px;
  background-color: #f5f5f5;
  display: flex;
  flex-direction: column;
  align-items: center;
  padding-top: 100px;
  gap: 0;
  z-index: 60;
}

.toolbar-icon {
  width: 56px;
  height: 56px;
  background-color: #fff;
  border: 1px solid #eee;
  border-left: none;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 20px;
  cursor: pointer;
  transition: all 0.2s;
  margin-bottom: -1px;
}

.toolbar-icon:hover {
  background-color: #ff5000;
  color: white;
  border-color: #ff5000;
}

@media (max-width: 1200px) {
  .right-sidebar {
    display: none;
  }

  .toolbar-icons {
    display: none;
  }
}
</style>
