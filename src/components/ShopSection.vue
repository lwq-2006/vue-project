<script setup>
import CartItem from './CartItem.vue'

const props = defineProps({
  shop: {
    type: Object,
    required: true
  }
})

const emit = defineEmits(['toggleShopCheck', 'toggleItemCheck', 'decreaseQuantity', 'increaseQuantity', 'deleteItem'])

const handleToggleShopCheck = () => {
  emit('toggleShopCheck', props.shop)
}

const handleToggleItemCheck = (item) => {
  emit('toggleItemCheck', props.shop, item)
}

const handleDecreaseQuantity = (item) => {
  emit('decreaseQuantity', item)
}

const handleIncreaseQuantity = (item) => {
  emit('increaseQuantity', item)
}

const handleDeleteItem = (item) => {
  emit('deleteItem', props.shop, item)
}
</script>

<template>
  <div class="shop-section">
    <div class="shop-header">
      <label class="shop-select">
        <input type="checkbox" :checked="shop.shopChecked" @change="handleToggleShopCheck" />
        <img v-if="shop.platform === '天猫'" class="platform-tag tmall" src="https://gw.alicdn.com/imgextra/i2/O1CN01Mo9BIf1DOOTmHgOR1_!!6000000000206-2-tps-102-48.png" alt="天猫">
        <img v-else class="platform-tag taobao" src="https://gw.alicdn.com/imgextra/i1/O1CN01pej3Sn25s9StSuv4K_!!6000000007581-2-tps-106-48.png" alt="淘宝">
        <span class="shop-name">{{ shop.shop }}</span>
      </label>
    </div>

    <div class="shop-items">
      <CartItem
        v-for="item in shop.items"
        :key="item.id"
        :item="item"
        :shop="shop"
        @toggle-check="handleToggleItemCheck"
        @decrease-quantity="handleDecreaseQuantity"
        @increase-quantity="handleIncreaseQuantity"
        @delete-item="handleDeleteItem"
      />
    </div>
  </div>
</template>

<style scoped>
.shop-section {
  border-bottom: 1px solid #f0f0f0;
  margin-bottom: 8px;
  padding-bottom: 8px;
}

.shop-section:last-child {
  border-bottom: none;
  margin-bottom: 0;
}

.shop-header {
  padding: 8px 0;
}

.shop-select {
  display: flex;
  align-items: center;
  gap: 8px;
  cursor: pointer;
}

.shop-select input[type="checkbox"] {
  width: 22px;
  height: 22px;
  cursor: pointer;
  border: 1px solid #f9f9f9;
  border-radius: 4px;
  accent-color: #ff5000;
  appearance: auto;
}

.platform-tag {
  display: inline-block;
  height: 14px;
  object-fit: contain;
}

.platform-tag.tmall {
  width: 28px;
}

.platform-tag.taobao {
  width: 30px;
}

.shop-name {
  font-size: 16px;
  font-weight: normal;
  color: #333;
}

.shop-name:hover {
  color: #ff5000;
}

.shop-items {
  padding: 0;
}
</style>