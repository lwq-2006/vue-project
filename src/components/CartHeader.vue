<template>
  <header class="header">
    <div class="header-top">
      <div class="header-links">
        <a href="#">tb50697...</a>
        <a href="#">网页无障碍</a>
        <span class="separator">|</span>
        <a href="#">淘宝网首页</a>
        <a href="#">已买到的宝贝</a>
        <a href="#">我的淘宝 <span class="arrow">▼</span></a>
        <a href="#">购物车 <span class="cart-count">10</span></a>
        <a href="#">收藏夹 <span class="arrow">▼</span></a>
        <span class="separator">|</span>
        <a href="#">免费开店</a>
        <a href="#">千牛卖家中心 <span class="arrow">▼</span></a>
        <a href="#">帮助中心 <span class="arrow">▼</span></a>
      </div>
    </div>
    <div class="header-main">
      <div class="header-left">
        <a href="#" class="logo">淘宝</a>
        <span class="cart-title">购物车</span>
      </div>
    </div>
  </header>
</template>

<style scoped>
.header {
  background-color: #f5f5f5;
  color: #666;
}

.header-top {
  max-width: 1200px;
  margin: 0 auto;
  padding: 8px 20px;
  display: flex;
  justify-content: flex-end;
  font-size: 12px;
}

.header-links {
  display: flex;
  align-items: center;
  gap: 12px;
}

.header-links a {
  color: #666;
  text-decoration: none;
  font-size: 12px;
}

.header-links a:hover {
  color: #ff5000;
}

.separator {
  color: #ddd;
}

.arrow {
  font-size: 10px;
  margin-left: 2px;
}

.cart-count {
  color: #ff5000;
  font-weight: bold;
}

.header-main {
  background-color: white;
  border-bottom: 1px solid #eee;
}

.header-main .header-left {
  max-width: 1200px;
  margin: 0 auto;
  padding: 20px;
  display: flex;
  align-items: center;
  gap: 16px;
}

.logo {
  font-size: 32px;
  font-weight: bold;
  color: #ff5000;
  text-decoration: none;
}

.cart-title {
  font-size: 20px;
  font-weight: 500;
  color: #333;
  border-left: 2px solid #eee;
  padding-left: 16px;
}
</style>
