<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

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

// 搜索提示词轮换
const searchPlaceholders = [
  '淡人高知穿搭一整套',
  '轻职场正装',
  '春日新款连衣裙',
  '复古牛仔外套',
  '舒适休闲运动鞋'
]
const currentPlaceholder = ref(searchPlaceholders[0])
let placeholderInterval = null

onMounted(() => {
  let index = 0
  placeholderInterval = setInterval(() => {
    index = (index + 1) % searchPlaceholders.length
    currentPlaceholder.value = searchPlaceholders[index]
  }, 3000)
})

onUnmounted(() => {
  if (placeholderInterval) {
    clearInterval(placeholderInterval)
  }
})
</script>

<template>
  <div class="right-sidebar">
    <!-- 搜索框 -->
    <div class="search-section">
      <div class="search-wrapper">
        <input type="text" class="search-input" :placeholder="currentPlaceholder" />
        <span class="camera-icon">
          <img src="data:image/png;base64,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" width="20" height="20" alt="相机" />
        </span>
      </div>
      <button class="search-btn">搜淘宝</button>
    </div>

    <!-- 结算卡片 -->
    <div class="checkout-card">
      <h3 class="checkout-title">结算明细</h3>
      
      <!-- 空状态 -->
      <div class="empty-state" v-if="selectedCount === 0">
        <div class="empty-cart-icon">
          <svg class="cart-svg" viewBox="0 0 1024 1024" width="70" height="70">
            <path fill="#e8e8e8" d="M832 320H704l-64-128H384l-64 128H192c-35.2 0-64 28.8-64 64v384c0 35.2 28.8 64 64 64h640c35.2 0 64-28.8 64-64V384c0-35.2-28.8-64-64-64z"/>
            <path fill="#d0d0d0" d="M352 448h320v64H352z"/>
            <path fill="#f5a623" d="M480 256h64v64h-64z"/>
            <path fill="#f5a623" d="M384 192h256v64H384z"/>
          </svg>
          <span class="empty-tag">空</span>
        </div>
        <p class="empty-tip">选择商品查看实际支付价格</p>
      </div>

      <!-- 有商品状态 -->
      <div class="price-detail" v-else>
        <div class="detail-row">
          <span class="detail-label">商品总价</span>
          <span class="detail-value">¥{{ totalPrice }}</span>
        </div>
      </div>

      <!-- 合计 -->
      <div class="total-section">
        <div class="total-label">合计:</div>
        <div class="total-price" :class="{ 'has-value': selectedCount > 0 }">
          <span class="currency">¥</span>{{ selectedCount > 0 ? totalPrice : '0' }}
        </div>
      </div>

      <!-- 结算按钮 -->
      <button class="checkout-btn" :disabled="selectedCount === 0">
        结算
      </button>
    </div>
  </div>

  <!-- 右侧工具栏 -->
  <div class="side-toolbar">
    <div class="toolbar-item">
      <img class="toolbar-icon" src="https://img.alicdn.com/imgextra/i2/O1CN01wHaWZy1FZ33onMlN9_!!6000000000500-2-tps-96-96.png" alt="首页">
      <span class="toolbar-text">首页</span>
    </div>
    <div class="toolbar-item">
      <img class="toolbar-icon" src="https://gw.alicdn.com/imgextra/i4/O1CN0165n4Cr1CGK2faBVbj_!!6000000000053-1-tps-56-56.gif" alt="桌面版">
      <span class="toolbar-text">桌面版</span>
    </div>
    <div class="toolbar-item">
      <img class="toolbar-icon" src="https://img.alicdn.com/imgextra/i1/O1CN01KKO3Hn1q6K0AhkkRK_!!6000000005446-2-tps-96-96.png" alt="消息">
      <span class="toolbar-text">消息</span>
    </div>
    <div class="toolbar-item">
      <img class="toolbar-icon" src="https://gw.alicdn.com/imgextra/i3/O1CN01js47DP1J3DxYBQG4g_!!6000000000972-1-tps-56-56.gif" alt="用户调研">
      <span class="toolbar-text">用户调研</span>
    </div>
    <div class="toolbar-item">
      <img class="toolbar-icon" src="https://img.alicdn.com/imgextra/i4/O1CN01mTKtIG1JNNQh0OvhC_!!6000000001016-2-tps-96-96.png" alt="我的淘宝">
      <span class="toolbar-text">我的淘宝</span>
    </div>
    <div class="toolbar-item">
      <img class="toolbar-icon" src="https://img.alicdn.com/imgextra/i2/O1CN01OReYno1rO0uvfo0fi_!!6000000005620-2-tps-96-96.png" alt="反馈">
      <span class="toolbar-text">反馈</span>
    </div>
  </div>
</template>

<style scoped>
.right-sidebar {
  position: fixed;
  right: 100px;
  top: 80px;
  width: 340px;
  z-index: 100;
}

/* 搜索区域 */
.search-section {
  display: flex;
  gap: 0;
  margin-bottom: 10px;
}

.search-wrapper {
  flex: 1;
  position: relative;
}

.search-input {
  width: 100%;
  padding: 10px 40px 10px 16px;
  border: 1px solid #e0e0e0;
  border-right: none;
  border-radius: 20px 0 0 20px;
  font-size: 14px;
  outline: none;
  background-color: #fff;
  color: #333;
}

.search-input::placeholder {
  color: #999;
  transition: opacity 0.3s;
}

.camera-icon {
  position: absolute;
  right: 10px;
  top: 50%;
  transform: translateY(-50%);
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  width: 24px;
  height: 24px;
}

.camera-icon img {
  width: 20px;
  height: 20px;
  opacity: 0.6;
}

.search-btn {
  background: linear-gradient(90deg, #ff9000 0%, #ff5000 100%);
  color: white;
  border: none;
  padding: 10px 20px;
  border-radius: 0 20px 20px 0;
  font-size: 14px;
  font-weight: bold;
  cursor: pointer;
  white-space: nowrap;
}

/* 结算卡片 */
.checkout-card {
  background-color: white;
  border-radius: 12px;
  padding: 20px;
  border: 1px solid #f0f0f0;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.04);
}

.checkout-title {
  font-size: 16px;
  font-weight: bold;
  color: #333;
  margin-bottom: 20px;
  text-align: left;
}

/* 空状态 */
.empty-state {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 30px 0 20px;
}

.empty-cart-icon {
  position: relative;
  margin-bottom: 12px;
}

.cart-svg {
  display: block;
}

.empty-tag {
  position: absolute;
  top: 5px;
  right: -5px;
  background: linear-gradient(135deg, #ffb088 0%, #ff8a5c 100%);
  color: white;
  font-size: 11px;
  padding: 3px 8px;
  border-radius: 50%;
  min-width: 20px;
  text-align: center;
  font-weight: 500;
}

.empty-tip {
  font-size: 16px;
  color: #ff6a3c;
  font-weight: bold;
}

/* 价格详情 */
.price-detail {
  padding: 10px 0;
  border-bottom: 1px dashed #e8e8e8;
  margin-bottom: 15px;
}

.detail-row {
  display: flex;
  justify-content: space-between;
  align-items: center;
  font-size: 14px;
}

.detail-label {
  color: #999;
}

.detail-value {
  color: #666;
  font-weight: 500;
}

/* 合计区域 */
.total-section {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
}

.total-label {
  font-size: 15px;
  font-weight: 500;
  color: #333;
}

.total-price {
  font-size: 22px;
  font-weight: bold;
  color: #ccc;
  display: flex;
  align-items: baseline;
}

.total-price .currency {
  font-size: 16px;
  margin-right: 2px;
}

.total-price.has-value {
  color: #ff5000;
}

.total-price.has-value .currency {
  color: #ff5000;
}

/* 结算按钮 */
.checkout-btn {
  width: 100%;
  padding: 12px;
  background-color: #ff5000;
  color: white;
  border: none;
  border-radius: 25px;
  font-size: 15px;
  font-weight: bold;
  cursor: pointer;
  transition: all 0.3s;
}

.checkout-btn:hover:not(:disabled) {
  background-color: #ff4400;
}

.checkout-btn:disabled {
  background-color: #ffb380;
  cursor: not-allowed;
}

/* 右侧工具栏 */
.side-toolbar {
  position: fixed;
  right: 0;
  bottom: 50%;
  transform: translateY(50%);
  z-index: 999;
  background-color: #fff;
  border-radius: 12px 0 0 12px;
  width: 56px;
  border: 1px solid rgba(0, 0, 0, 0.08);
  border-right: none;
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 12px 0;
  box-shadow: -1px 0 5px rgba(0, 0, 0, 0.05);
}

.toolbar-item {
  position: relative;
  text-align: center;
  width: 48px;
  height: 48px;
  margin-top: 8px;
  z-index: 1;
  cursor: pointer;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  transition: all 0.2s;
  margin-left: 4px;
}

.toolbar-item:hover {
  background-color: #f5f5f5;
}

.toolbar-item.active {
  background-color: #f5f5f5;
}

.toolbar-item.active .toolbar-text {
  color: #ff5000;
}

.toolbar-icon {
  display: block;
  width: 24px;
  height: 24px;
  object-fit: contain;
  margin-bottom: 2px;
}

.toolbar-text {
  font-size: 11px;
  color: #666;
}

.badge {
  position: absolute;
  top: 8px;
  right: 8px;
  background-color: #ff4d4f;
  color: white;
  font-size: 10px;
  padding: 1px 5px;
  border-radius: 8px;
  min-width: 16px;
  text-align: center;
}

@media (max-width: 1200px) {
  .right-sidebar,
  .side-toolbar {
    display: none;
  }
}
</style>
