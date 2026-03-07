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
      <div class="shop-select">
        <input type="checkbox" :checked="shop.shopChecked" @change="handleToggleShopCheck" :id="'shop-' + shop.id" />
        <span class="shop-platform" v-if="shop.platform">{{ shop.platform }}</span>
        <label :for="'shop-' + shop.id" class="shop-name">{{ shop.shop }}</label>
      </div>
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
  border-bottom: 1px solid #eee;
  margin-bottom: 12px;
}

.shop-section:last-child {
  border-bottom: none;
  margin-bottom: 0;
}

.shop-header {
  padding: 12px 0;
}

.shop-select {
  display: flex;
  align-items: center;
  gap: 8px;
}

.shop-select input[type="checkbox"] {
  width: 18px;
  height: 18px;
  cursor: pointer;
}

.shop-platform {
  display: inline-block;
  padding: 2px 6px;
  background-color: #ff5000;
  color: white;
  font-size: 11px;
  border-radius: 2px;
}

.shop-name {
  font-size: 14px;
  font-weight: 500;
  color: #333;
  cursor: pointer;
}

.shop-name:hover {
  color: #ff5000;
}

.shop-items {
  padding: 0;
}
</style>
