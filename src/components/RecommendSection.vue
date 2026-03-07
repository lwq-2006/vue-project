<script setup>
const props = defineProps({
  recommendItems: {
    type: Array,
    required: true
  }
})
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
          <div class="recommend-name">{{ item.name }}</div>
          <div class="recommend-price">¥{{ item.price.toFixed(2) }}</div>
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
  font-size: 16px;
  color: #333;
  font-weight: 500;
}

.recommend-list {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 20px;
}

.recommend-item {
  cursor: pointer;
  transition: transform 0.2s, box-shadow 0.2s;
}

.recommend-item:hover {
  transform: translateY(-4px);
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
}

.recommend-image {
  width: 100%;
  padding-bottom: 100%;
  position: relative;
  overflow: hidden;
  border-radius: 4px;
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
  padding: 12px 8px;
}

.recommend-name {
  font-size: 13px;
  color: #333;
  line-height: 1.4;
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  overflow: hidden;
  margin-bottom: 8px;
}

.recommend-price {
  font-size: 16px;
  font-weight: bold;
  color: #ff5000;
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
