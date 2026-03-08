<script setup>
import { ref, computed, onMounted } from 'vue'

const props = defineProps({
  cartItemCount: {
    type: Number,
    default: 0
  }
})

const showUserPopup = ref(false)
const showTaobaoPopup = ref(false)
const showFavoritesPopup = ref(false)
const showFreeShopPopup = ref(false)
const showSellerPopup = ref(false)
const showHelpPopup = ref(false)

const handleMouseEnter = (popup) => {
  popup.value = true
}

const handleMouseLeave = (popup) => {
  popup.value = false
}
</script>

<template>
  <header class="header">
    <!-- 顶部导航栏 -->
    <div class="header-top">
      <div class="header-links">
        <!-- 左侧链接 -->
        <div class="header-links-left">
          <div class="user-link" @mouseenter="handleMouseEnter(showUserPopup)" @mouseleave="handleMouseLeave(showUserPopup)">
            <a href="#" class="user-id">tb50697...</a>
            <div v-if="showUserPopup" class="popup user-popup">
              <div class="popup-content">
                <div class="user-avatar">
                  <img src="https://img.alicdn.com/imgextra/i3/O1CN01k9X6X61X6X6X6X6X_!!6000000000000-0-tps-100-100.jpg" alt="用户头像">
                </div>
                <div class="user-info">
                  <div class="user-id">tb5069873292</div>
                  <div class="user-actions">
                    <a href="#">账号管理</a>
                    <span>|</span>
                    <a href="#">退出</a>
                  </div>
                  <div class="user-benefit">
                    <a href="#">查看你的专属权益</a>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <a href="#">网页无障碍</a>
        </div>
        <!-- 右侧链接 -->
        <div class="header-links-right">
          <a href="#">淘宝网首页</a>
          <a href="#">已买到的宝贝</a>
          <div class="dropdown-link" @mouseenter="handleMouseEnter(showTaobaoPopup)" @mouseleave="handleMouseLeave(showTaobaoPopup)">
            <a href="#" class="dropdown">我的淘宝 <span class="arrow">▼</span></a>
            <div v-if="showTaobaoPopup" class="popup taobao-popup">
              <div class="popup-content">
                <a href="#">我的足迹</a>
                <a href="#">我的卡券包</a>
              </div>
            </div>
          </div>
          <a href="#" class="cart-link">
            <img class="cart-icon" src="https://img.alicdn.com/imgextra/i2/O1CN01wHaWZy1FZ33onMlN9_!!6000000000500-2-tps-96-96.png" alt="购物车">
            <span class="cart-text">购物车</span>
            <span class="cart-count">{{ cartItemCount || 10 }}</span>
          </a>
          <div class="dropdown-link" @mouseenter="handleMouseEnter(showFavoritesPopup)" @mouseleave="handleMouseLeave(showFavoritesPopup)">
            <a href="#" class="dropdown">✰ 收藏夹 <span class="arrow">▼</span></a>
            <div v-if="showFavoritesPopup" class="popup favorites-popup">
              <div class="popup-content">
                <a href="#">收藏的宝贝</a>
                <a href="#">收藏的店铺</a>
              </div>
            </div>
          </div>
          <div class="dropdown-link" @mouseenter="handleMouseEnter(showFreeShopPopup)" @mouseleave="handleMouseLeave(showFreeShopPopup)">
            <a href="#">免费开店 <span class="arrow">▼</span></a>
            <div v-if="showFreeShopPopup" class="popup free-shop-popup">
              <div class="popup-content">
                <a href="#">淘宝开店</a>
                <a href="#">天猫开店</a>
                <a href="#">开直播店</a>
              </div>
            </div>
          </div>
          <div class="dropdown-link" @mouseenter="handleMouseEnter(showSellerPopup)" @mouseleave="handleMouseLeave(showSellerPopup)">
            <a href="#" class="dropdown">千牛卖家中心 <span class="arrow">▼</span></a>
            <div v-if="showSellerPopup" class="popup seller-popup">
              <div class="popup-content">
                <a href="#">开店入驻</a>
                <a href="#">已卖出的宝贝</a>
                <a href="#">出售中的宝贝</a>
                <a href="#">卖家服务市场</a>
                <a href="#">卖家培训中心</a>
                <a href="#">体验中心</a>
                <a href="#">电商学习中心</a>
              </div>
            </div>
          </div>
          <div class="dropdown-link" @mouseenter="handleMouseEnter(showHelpPopup)" @mouseleave="handleMouseLeave(showHelpPopup)">
            <a href="#" class="dropdown">帮助中心 <span class="arrow">▼</span></a>
            <div v-if="showHelpPopup" class="popup help-popup">
              <div class="popup-content">
                <a href="#">官方客服</a>
                <a href="#">商家客服</a>
                <a href="#">消息中心</a>
                <a href="#">意见反馈</a>
                <a href="#">举报中心</a>
                <a href="#">淘宝规则</a>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    
    <!-- 搜索栏 -->
    <div class="header-main">
      <div class="header-content">
        <div class="logo-section">
          <a href="#" class="logo">
            <img src="https://gw.alicdn.com/imgextra/i2/O1CN0188c2Ev1uamjpGQBxv_!!6000000006054-2-tps-252-120.png" alt="淘宝">
          </a>
          <span class="cart-title">购物车</span>
        </div>

      </div>
    </div>
  </header>
</template>

<style scoped>
.header {
  background-color: white;
  z-index: 100;
  margin: auto;
  max-width: 1680px;
  padding-left: 0;
  padding-right: 0;
  position: relative;
}

/* 顶部导航栏 */
.header-top {
  width: 100%;
  height: 35px;
  background: #fff;
  box-sizing: border-box;
  -webkit-backface-visibility: hidden;
  display: flex;
  font-size: 12px;
}

.header-links {
  display: flex;
  align-items: center;
  justify-content: space-between;
  width: 100%;
}

.header-links-left {
  display: flex;
  align-items: center;
  gap: 16px;
  flex-shrink: 0;
}

.header-links-right {
  display: flex;
  align-items: center;
  gap: 16px;
  flex-shrink: 0;
}

.header-links a {
  float: left;
  margin-right: 4px;
  font-size: 12px;
  color: #333;
  text-decoration: none;
  transition: color 0.2s;
}

.header-links a:hover {
  color: #ff5000;
}

.header-links-left a,
.header-links-right a {
  color: #333;
}

.header-links-left a:hover,
.header-links-right a:hover {
  color: #ff5000;
}

.user-id {
  color: #ff5000 !important;
}

.dropdown-link {
  position: relative;
}

.user-link {
  position: relative;
}

.popup {
  position: absolute;
  top: 100%;
  right: 0;
  margin-top: 4px;
  background-color: white;
  border: 1px solid #ddd;
  box-shadow: 0 2px 8px rgba(0,0,0,0.15);
  border-radius: 4px;
  padding: 12px;
  z-index: 1000;
  min-width: 160px;
}

.user-popup {
  right: -20px;
  min-width: 200px;
}

.popup-content {
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.user-popup .popup-content {
  flex-direction: row;
  align-items: center;
  gap: 16px;
}

.user-avatar {
  width: 48px;
  height: 48px;
  border-radius: 50%;
  overflow: hidden;
}

.user-avatar img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.user-info {
  flex: 1;
}

.user-actions {
  font-size: 12px;
  margin-bottom: 8px;
}

.user-actions a {
  margin: 0 4px;
}

.user-benefit {
  margin-top: 8px;
}

.user-benefit a {
  font-size: 12px;
  color: #ff5000;
  text-decoration: underline;
}

.cart-link {
  display: flex;
  align-items: center;
  gap: 4px;
}

.cart-icon {
  width: 14px;
  height: 14px;
  object-fit: contain;
}

.cart-text {
  color: #ff5000;
  font-weight: 500;
}

.cart-count {
  color: #ff5000;
  font-weight: bold;
}

.dropdown .arrow {
  font-size: 10px;
  margin-left: 2px;
}

/* 搜索栏 */
.header-main {
  background-color: white;
  padding: 20px 0 0 0;
}

.header-content {
  width: 100%;
  display: flex;
  align-items: center;
  gap: 40px;
}

.logo-section {
  display: flex;
  align-items: center;
  gap: 12px;
  flex-shrink: 0;
}

.logo {
  text-decoration: none;
  display: inline-block;
}

.logo img {
  height: 40px;
  object-fit: contain;
}

.cart-title {
  color: #ff5000;
  font-size: 24px;
  font-weight: 600;
}



@media screen and (max-width: 1440px) {
  .header {
    padding-left: 10px;
    padding-right: 10px;
  }
}

@media screen and (max-width: 1240px) {
  .header {
    min-width: 780px;
  }
}

@media (max-width: 768px) {
  .header-top {
    display: none;
  }
  
  .header-content {
    flex-direction: column;
    gap: 16px;
  }
}
</style>