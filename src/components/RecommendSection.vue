<script setup>
const props = defineProps({
  recommendItems: {
    type: Array,
    required: true
  }
})

// 底部横向标签
const bottomTags = [
  { name: '赛事直播', bgColor: '#ff6b6b', textColor: '#fff' },
  { name: '创意洗碗海绵', bgColor: '#4ecdc4', textColor: '#fff' },
  { name: '乌龟晒台爬台', bgColor: '#45b7d1', textColor: '#fff' },
  { name: '316内胆保温杯', bgColor: '#96ceb4', textColor: '#fff' },
  { name: '运动套装女', bgColor: '#feca57', textColor: '#333' },
  { name: '盲盒手办', bgColor: '#ff9ff3', textColor: '#fff' },
  { name: '零食大礼包', bgColor: '#54a0ff', textColor: '#fff' }
]
</script>

<template>
  <div class="recommend-section">
    <div class="recommend-header">
      <h3>猜你喜欢</h3>
    </div>
    <div class="recommend-list">
      <div v-for="item in recommendItems" :key="item.id" class="recommend-item">
        <div class="recommend-image">
          <img :src="item.image" :alt="item.name" />
        </div>
        <div class="recommend-info">
          <div class="recommend-name">
            <span v-if="item.platform" class="platform-tag" :class="item.platform">{{ item.platform === 'tmall' ? '天猫' : '淘宝' }}</span>
            <span class="name-text">{{ item.name }}</span>
          </div>
          <div v-if="item.promoTags && item.promoTags.length" class="promo-tags">
            <span v-for="(tag, idx) in item.promoTags" :key="idx" class="promo-tag">{{ tag }}</span>
          </div>
          <div class="recommend-price">
            <span class="price-symbol">¥</span>
            <span class="price-value">{{ item.price.toFixed(2) }}</span>
          </div>
          <div v-if="item.sales" class="recommend-sales">{{ item.sales }}</div>
        </div>
      </div>
    </div>
    
    <!-- 底部横向滚动标签 -->
    <div class="bottom-tags-wrapper">
      <div class="bottom-tags">
        <div v-for="(tag, idx) in bottomTags" :key="idx" class="bottom-tag" :style="{ backgroundColor: tag.bgColor, color: tag.textColor }">
          {{ tag.name }}
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.recommend-section {
  background-color: white;
  border-radius: 4px;
  padding: 20px;
  margin-top: 20px;
}

.recommend-header {
  margin-bottom: 20px;
}

.recommend-header h3 {
  font-size: 18px;
  color: #333;
  font-weight: 600;
}

.recommend-list {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 16px;
}

.recommend-item {
  cursor: pointer;
  transition: transform 0.2s, box-shadow 0.2s;
  border-radius: 8px;
  overflow: hidden;
}

.recommend-item:hover {
  transform: translateY(-4px);
  box-shadow: 0 4px 16px rgba(0, 0, 0, 0.12);
}

.recommend-image {
  width: 100%;
  padding-bottom: 100%;
  position: relative;
  overflow: hidden;
  background-color: #f5f5f5;
}

.recommend-image img {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.recommend-info {
  padding: 10px 8px;
}

.recommend-name {
  font-size: 13px;
  color: #333;
  line-height: 1.5;
  display: -webkit-box;
  -webkit-line-clamp: 2;
  line-clamp: 2;
  -webkit-box-orient: vertical;
  overflow: hidden;
  margin-bottom: 6px;
}

.platform-tag {
  display: inline-flex;
  align-items: center;
  padding: 0 3px;
  border-radius: 3px;
  font-size: 11px;
  font-weight: bold;
  margin-right: 4px;
  vertical-align: middle;
}

.platform-tag.tmall {
  background-color: #ff0036;
  color: white;
}

.platform-tag.taobao {
  background-color: #ff5000;
  color: white;
}

.name-text {
  vertical-align: middle;
}

.promo-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 4px;
  margin-bottom: 6px;
}

.promo-tag {
  font-size: 11px;
  color: #ff5000;
  background-color: #fff0e8;
  padding: 1px 4px;
  border-radius: 2px;
}

.recommend-price {
  display: flex;
  align-items: baseline;
  margin-bottom: 4px;
}

.price-symbol {
  font-size: 12px;
  color: #ff5000;
  margin-right: 1px;
}

.price-value {
  font-size: 18px;
  font-weight: bold;
  color: #ff5000;
}

.recommend-sales {
  font-size: 12px;
  color: #999;
}

/* 底部横向标签 */
.bottom-tags-wrapper {
  margin-top: 24px;
  padding-top: 16px;
  border-top: 1px solid #f0f0f0;
}

.bottom-tags {
  display: flex;
  gap: 12px;
  overflow-x: auto;
  padding-bottom: 8px;
}

.bottom-tags::-webkit-scrollbar {
  height: 4px;
}

.bottom-tags::-webkit-scrollbar-thumb {
  background-color: #ddd;
  border-radius: 2px;
}

.bottom-tag {
  flex-shrink: 0;
  padding: 8px 16px;
  border-radius: 16px;
  font-size: 13px;
  font-weight: 600;
  cursor: pointer;
  transition: transform 0.2s, opacity 0.2s;
}

.bottom-tag:hover {
  transform: scale(1.05);
  opacity: 0.9;
}

@media (max-width: 1024px) {
  .recommend-list {
    grid-template-columns: repeat(3, 1fr);
  }
}

@media (max-width: 768px) {
  .recommend-list {
    grid-template-columns: repeat(2, 1fr);
  }
}
</style>
