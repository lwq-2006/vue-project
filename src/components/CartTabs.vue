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
    <div 
      v-for="tab in tabs" 
      :key="tab.id" 
      class="tab-item" 
      :class="{ active: activeTab === tab.id }" 
      @click="handleTabClick(tab)"
    >
      <img v-if="tab.id === 'all'" class="tab-icon" src="https://img.alicdn.com/imgextra/i3/O1CN01cSckuL1rZ0SuPp3CW_!!6000000005644-2-tps-48-48.png" alt="全部商品">
      <img v-else-if="tab.id === 'coupon'" class="tab-icon" src="https://img.alicdn.com/imgextra/i4/O1CN01K54O2W1kDINaR0LwX_!!6000000004649-2-tps-48-48.png" alt="消费券">
      <img v-else-if="tab.id === 'official'" class="tab-icon" src="https://img.alicdn.com/imgextra/i3/O1CN01T5ZiCp28x8o4g7Fjp_!!6000000007998-2-tps-96-96.png" alt="官方立减">
      <img v-else-if="tab.id === 'super'" class="tab-icon" src="https://img.alicdn.com/imgextra/i1/O1CN01JMB2HG1lBkfGrHJ01_!!6000000004781-2-tps-96-96.png" alt="超级立减">
      <img v-else-if="tab.id === 'sale'" class="tab-icon" src="https://img.alicdn.com/imgextra/i4/O1CN01QEA5sq1NHCayKabd0_!!6000000001544-2-tps-48-48.png" alt="降价">
      <span class="tab-name">{{ tab.name }}</span>
      <span v-if="tab.count" class="tab-count">({{ tab.count }})</span>
    </div>
  </div>
</template>

<style scoped>
.cart-tabs {
  display: flex;
  gap: 8px;
  padding: 13px 0;
}

.tab-item {
  display: flex;
  align-items: center;
  gap: 0;
  font-size: 17px;
  color: #333;
  font-weight: normal;
  cursor: pointer;
  height: 48px;
  padding-bottom: 12px;
  border-bottom: 2px solid transparent;
  border-top: 2px solid transparent;
  margin-bottom: -16px;
  margin-right: 32px;
  position: relative;
  box-sizing: border-box;
  flex-shrink: 0;
  transition: all 0.2s;
}

.tab-item:hover {
  color: #ff5000;
}

.tab-item.active {
  color: #ff5000;
  border-bottom-color: #ff5000;
  font-weight: 600;
}

.tab-icon {
  width: 24px;
  height: 24px;
  object-fit: contain;
  margin-right: 2px;
}

.tab-name {
  font-size: 17px;
}

.tab-count {
  font-size: 17px;
}
</style>