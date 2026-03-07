<script setup>
import { ref } from 'vue'

const activeTab = ref('all')

const tabs = [
  { id: 'all', name: '全部商品', count: 10 },
  { id: 'coupon', name: '消费券' },
  { id: 'official', name: '官方立减' },
  { id: 'super', name: '超级立减' },
  { id: 'sale', name: '降价' }
]

const emit = defineEmits(['changeTab'])

const handleTabClick = (tab) => {
  activeTab.value = tab.id
  emit('changeTab', tab.id)
}
</script>

<template>
  <div class="cart-tabs">
    <div v-for="tab in tabs" :key="tab.id" class="tab-item" :class="{ active: activeTab === tab.id }" @click="handleTabClick(tab)">
      <span v-if="tab.id === 'all'" class="tab-icon">🧡</span>
      <span v-else-if="tab.id === 'coupon'" class="tab-icon">🎫</span>
      <span v-else-if="tab.id === 'official'" class="tab-icon">💎</span>
      <span v-else-if="tab.id === 'super'" class="tab-icon">⬇️</span>
      <span v-else-if="tab.id === 'sale'" class="tab-icon">⚡</span>
      <span class="tab-name">{{ tab.name }}</span>
      <span v-if="tab.count" class="tab-count">({{ tab.count }})</span>
    </div>
  </div>
</template>

<style scoped>
.cart-tabs {
  display: flex;
  gap: 32px;
  padding: 16px 0;
  border-bottom: 2px solid #eee;
}

.tab-item {
  display: flex;
  align-items: center;
  gap: 6px;
  font-size: 16px;
  color: #666;
  cursor: pointer;
  padding-bottom: 14px;
  border-bottom: 2px solid transparent;
  margin-bottom: -16px;
  transition: all 0.2s;
}

.tab-item:hover {
  color: #ff5000;
}

.tab-item.active {
  color: #ff5000;
  border-bottom-color: #ff5000;
  font-weight: 500;
}

.tab-icon {
  font-size: 18px;
}

.tab-name {
  font-size: 16px;
}

.tab-count {
  color: #ff5000;
  font-size: 14px;
}
</style>
