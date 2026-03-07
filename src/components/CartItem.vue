<script setup>
const props = defineProps({
  item: {
    type: Object,
    required: true
  },
  shop: {
    type: Object,
    required: true
  }
})

const emit = defineEmits(['toggleCheck', 'decreaseQuantity', 'increaseQuantity', 'deleteItem'])

const handleToggleCheck = () => {
  emit('toggleCheck', props.item)
}

const handleDecreaseQuantity = () => {
  emit('decreaseQuantity', props.item)
}

const handleIncreaseQuantity = () => {
  emit('increaseQuantity', props.item)
}

const handleDeleteItem = () => {
  emit('deleteItem', props.item)
}
</script>

<template>
  <div class="cart-item">
    <div class="item-select">
      <input type="checkbox" :checked="item.checked" @change="handleToggleCheck" :id="'item-' + item.id" />
    </div>
    <div class="item-image">
      <img :src="item.image" :alt="item.name" />
    </div>
    <div class="item-main">
      <div class="item-info">
        <div class="item-name">{{ item.name }}</div>
        <div class="item-spec">
          <span v-if="item.tags" class="item-tags">
            <span v-for="(tag, index) in item.tags" :key="index" class="tag">{{ tag }}</span>
          </span>
          <span>{{ item.spec }}</span>
        </div>
      </div>
      <div class="item-price-section">
        <div class="price-info">
          <span class="price">¥{{ item.price.toFixed(2) }}</span>
          <span class="original-price" v-if="item.originalPrice > item.price">¥{{ item.originalPrice.toFixed(2) }}</span>
        </div>
        <div class="quantity-control">
          <button class="quantity-btn" @click="handleDecreaseQuantity" :disabled="item.quantity <= 1">-</button>
          <input type="text" :value="item.quantity" readonly class="quantity-input" />
          <button class="quantity-btn" @click="handleIncreaseQuantity">+</button>
        </div>
      </div>
      <div class="item-total-price">
        <span class="total">¥{{ (item.price * item.quantity).toFixed(2) }}</span>
      </div>
      <div class="item-actions">
        <button class="action-btn" @click="handleDeleteItem">删除</button>
        <button class="action-btn">移入收藏</button>
      </div>
    </div>
  </div>
</template>

<style scoped>
.cart-item {
  display: flex;
  gap: 16px;
  padding: 20px 0;
  border-bottom: 1px solid #f5f5f5;
}

.cart-item:last-child {
  border-bottom: none;
}

.item-select {
  display: flex;
  align-items: flex-start;
  padding-top: 4px;
}

.item-select input[type="checkbox"] {
  width: 18px;
  height: 18px;
  cursor: pointer;
}

.item-image {
  width: 80px;
  height: 80px;
  flex-shrink: 0;
}

.item-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  border: 1px solid #eee;
  border-radius: 4px;
}

.item-main {
  flex: 1;
  display: flex;
  gap: 24px;
}

.item-info {
  flex: 2;
}

.item-name {
  font-size: 14px;
  color: #333;
  line-height: 1.5;
  margin-bottom: 8px;
}

.item-spec {
  font-size: 12px;
  color: #999;
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
}

.item-tags {
  display: flex;
  gap: 4px;
}

.tag {
  display: inline-block;
  padding: 2px 6px;
  background-color: #fff0f0;
  color: #ff5000;
  font-size: 11px;
  border-radius: 2px;
}

.item-price-section {
  flex: 1;
  display: flex;
  flex-direction: column;
  gap: 12px;
  align-items: flex-start;
}

.price-info {
  display: flex;
  align-items: baseline;
  gap: 8px;
}

.price {
  font-size: 16px;
  font-weight: bold;
  color: #ff5000;
}

.original-price {
  font-size: 12px;
  color: #999;
  text-decoration: line-through;
}

.quantity-control {
  display: flex;
  align-items: center;
}

.quantity-btn {
  width: 28px;
  height: 28px;
  border: 1px solid #ddd;
  background-color: #fff;
  cursor: pointer;
  font-size: 14px;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 4px 0 0 4px;
}

.quantity-btn:last-child {
  border-radius: 0 4px 4px 0;
}

.quantity-btn:hover:not(:disabled) {
  background-color: #f5f5f5;
}

.quantity-btn:disabled {
  color: #ccc;
  cursor: not-allowed;
}

.quantity-input {
  width: 40px;
  height: 28px;
  border: 1px solid #ddd;
  border-left: none;
  border-right: none;
  text-align: center;
  font-size: 14px;
  outline: none;
}

.item-total-price {
  flex: 1;
  text-align: right;
}

.total {
  font-size: 16px;
  font-weight: bold;
  color: #ff5000;
}

.item-actions {
  flex: 0 0 auto;
  display: flex;
  flex-direction: column;
  gap: 8px;
  align-items: flex-end;
}

.action-btn {
  background: none;
  border: none;
  color: #666;
  font-size: 12px;
  cursor: pointer;
  white-space: nowrap;
}

.action-btn:hover {
  color: #ff5000;
}

@media (max-width: 768px) {
  .cart-item {
    flex-wrap: wrap;
  }

  .item-main {
    flex-wrap: wrap;
  }

  .item-info {
    width: 100%;
  }

  .item-price-section {
    width: 100%;
    flex-direction: row;
    justify-content: space-between;
    align-items: center;
  }

  .item-total-price {
    text-align: left;
  }

  .item-actions {
    width: 100%;
    flex-direction: row;
    justify-content: flex-end;
  }
}
</style>
