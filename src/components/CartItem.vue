<script setup>
import { ref } from 'vue'

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

const showImagePopup = ref(false)
const showTitleHover = ref(false)
const showSpecHover = ref(false)
const hoveredTag = ref(null)

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

const handleQuantityChange = (event) => {
  const value = parseInt(event.target.value)
  if (!isNaN(value) && value > 0) {
    props.item.quantity = value
  } else {
    props.item.quantity = 1
  }
}
</script>

<template>
  <div class="cart-item">
    <div class="item-row">
      <!-- 选择框 -->
      <div class="item-select">
        <input type="checkbox" :checked="item.checked" @change="handleToggleCheck" />
      </div>
      
      <!-- 商品图片 -->
      <div class="item-image-wrapper" @mouseenter="showImagePopup = true" @mouseleave="showImagePopup = false">
        <div class="item-image">
          <img :src="item.image" :alt="item.name" />
        </div>
        <div class="image-popup" v-show="showImagePopup">
          <img :src="item.image" :alt="item.name" />
        </div>
      </div>
      
      <!-- 商品信息 -->
      <div class="item-info">
        <div class="title-tags-section">
          <div class="item-title" @mouseenter="showTitleHover = true" @mouseleave="showTitleHover = false">
            {{ item.name }}
          </div>
          <div class="item-tags-row" v-if="item.tags && item.tags.length">
          <div v-for="(tag, index) in item.tags" :key="index" class="tag-container" @mouseenter="hoveredTag = index" @mouseleave="hoveredTag = null">
            <span class="tag">{{ tag }}</span>
            <div class="tag-popup" v-if="hoveredTag === index">
              <span>{{ tag }}</span>
            </div>
          </div>
        </div>
      </div>
        <div class="item-spec" @mouseenter="showSpecHover = true" @mouseleave="showSpecHover = false">
          <span v-if="showSpecHover" class="modify-btn">修改</span>
          <div class="spec-content">
            {{ item.spec }}
          </div>
        </div>
      </div>
      
      <!-- 价格区域 -->
      <div class="item-price-col">
        <div class="price-row">
          <span v-if="item.couponPrice < item.price" class="coupon-badge">券后价</span>
          <span class="current-price">¥{{ item.price.toFixed(2) }}</span>
        </div>
        <div class="original-price-row" v-if="item.originalPrice > item.price">
          <span class="original-price">¥{{ item.originalPrice.toFixed(2) }}</span>
        </div>
      </div>
      
      <!-- 数量控制 -->
      <div class="item-quantity-col">
        <div class="quantity-control">
          <button class="quantity-btn minus" @click="handleDecreaseQuantity" :disabled="item.quantity <= 1">-</button>
          <input type="text" v-model="item.quantity" @input="handleQuantityChange" class="quantity-input" />
          <button class="quantity-btn plus" @click="handleIncreaseQuantity">+</button>
        </div>
      </div>
      
      <!-- 操作 -->
      <div class="item-actions-col">
        <button class="action-link">移入收藏</button>
        <button class="action-link" @click="handleDeleteItem">删除</button>
      </div>
    </div>
  </div>
</template>

<style scoped>
.cart-item {
  padding: 16px 0;
  border-bottom: 1px solid #f5f5f5;
}

.cart-item:last-child {
  border-bottom: none;
}

.item-row {
  display: flex;
  align-items: flex-start;
  gap: 12px;
}

/* 选择框 */
.item-select {
  padding-top: 30px;
  flex-shrink: 0;
}

.item-select input[type="checkbox"] {
  width: 22px;
  height: 22px;
  cursor: pointer;
  border: 1px solid #f9f9f9;
  border-radius: 4px;
  accent-color: #ff5000;
  appearance: auto;
}

/* 商品图片包装器 */
.item-image-wrapper {
  position: relative;
  flex-shrink: 0;
  cursor: pointer;
}

/* 商品图片 */
.item-image {
  width: 80px;
  height: 80px;
  border-radius: 4px;
  overflow: hidden;
  border: 1px solid #f0f0f0;
}

.item-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.image-popup {
  position: absolute;
  top: -20px;
  left: 100%;
  margin-left: 10px;
  width: 300px;
  height: 300px;
  border: 1px solid #f0f0f0;
  border-radius: 8px;
  overflow: hidden;
  box-shadow: 0 4px 16px rgba(0, 0, 0, 0.15);
  z-index: 1000;
  background: white;
  padding: 10px;
}

.image-popup img {
  width: 100%;
  height: 100%;
  object-fit: contain;
}

/* 商品信息 */
.item-info {
  flex-grow: 0.8;
  flex-shrink: 1;
  margin-right: 16px;
  width: calc(100% - 500px);
  min-width: 0;
  margin-left: 5px;
  display: flex;
  gap: 16px;
}

.title-tags-section {
  flex: 0 0 50%;
  min-width: 0;
}

.item-spec {
  width: 120px;
  flex-shrink: 0;
}

.item-title {
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  color: #1f1f1f;
  cursor: pointer;
  display: -webkit-box;
  font-size: 14px;
  font-weight: 500;
  overflow: hidden;
  text-overflow: ellipsis;
  text-align: left;
}

.item-title:hover {
  color: #ff5000;
}

.item-tags-row {
  color: #ff5000;
  font-size: 14px;
  white-space: nowrap;
  margin-bottom: 6px;
  margin-left: 0;
  padding-left: 0;
  position: relative;
  z-index: 1;
}

.tag-container {
  display: inline-block;
  margin-right: 10px;
  position: relative;
  cursor: pointer;
}

.tag {
  display: inline-block;
  font-size: 14px;
  color: #ff5000;
}

.tag-popup {
  position: absolute;
  top: 100%;
  left: 0;
  margin-top: 5px;
  background: white;
  border: 1px solid #f0f0f0;
  border-radius: 4px;
  padding: 8px 12px;
  font-size: 12px;
  color: #333;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
  z-index: 9999;
  white-space: nowrap;
  max-width: 200px;
  transform: translateY(0);
  transition: all 0.3s ease;
}

.tag-container:hover .tag-popup {
  transform: translateY(-2px);
  box-shadow: 0 6px 16px rgba(0, 0, 0, 0.2);
}

.popup-item {
  padding: 4px 0;
  border-bottom: 1px solid #f5f5f5;
}

.popup-item:last-child {
  border-bottom: none;
}

.item-spec {
  box-sizing: border-box;
  width: 140px;
  height: 90px;
  padding: 5px 12px;
  position: relative;
  font-size: 12px;
  color: #999;
  line-height: 1.5;
  cursor: pointer;
  border-radius: 8px;
  transition: all 0.3s;
  border: none;
  margin-left: 15px;
}

.item-spec:hover {
  border: 1px dashed #ff5000;
}

.modify-btn {
  position: absolute;
  top: 0;
  right: 0;
  font-size: 10px;
  color: #ff5000;
  background: white;
  padding: 2px 4px;
}

.spec-content {
  margin-top: 0;
}

/* 价格列 */
.item-price-col {
  width: 100px;
  flex-shrink: 0;
  text-align: left;
  margin-left: -35px;
  padding-top: 20px;
}

.price-row {
  display: flex;
  align-items: center;
  gap: 4px;
  margin-bottom: 4px;
}

.coupon-badge {
  display: inline-block;
  background: linear-gradient(90deg, #ff9000 0%, #ff5000 100%);
  color: white;
  padding: 1px 4px;
  font-size: 10px;
  border-radius: 2px;
  font-weight: 500;
}

.current-price {
  font-size: 14px;
  font-weight: bold;
  color: #ff5000;
}

.original-price-row {
  font-size: 12px;
  color: #999;
}

.original-price {
  text-decoration: line-through;
}

/* 数量列 */
.item-quantity-col {
  width: 100px;
  flex-shrink: 0;
  margin-left: -10px;
  padding-top: 20px;
}

.quantity-control {
  display: flex;
  align-items: center;
  border: 1px solid #e8e8e8;
  border-radius: 4px;
  overflow: hidden;
}

.quantity-btn {
  width: 26px;
  height: 26px;
  border: none;
  background-color: #fafafa;
  cursor: pointer;
  font-size: 14px;
  color: #666;
  display: flex;
  align-items: center;
  justify-content: center;
}

.quantity-btn:hover:not(:disabled) {
  background-color: #f0f0f0;
}

.quantity-btn:disabled {
  color: #ccc;
  cursor: not-allowed;
}

.quantity-input {
  width: 36px;
  height: 26px;
  border: none;
  border-left: 1px solid #e8e8e8;
  border-right: 1px solid #e8e8e8;
  text-align: center;
  font-size: 13px;
  color: #333;
  background-color: white;
}

.quantity-input:focus {
  outline: none;
}

/* 操作列 */
.item-actions-col {
  width: 70px;
  flex-shrink: 0;
  display: flex;
  flex-direction: column;
  gap: 8px;
  align-items: center;
  padding-top: 20px;
}

.action-link {
  background: none;
  border: none;
  color: #666;
  font-size: 14px;
  cursor: pointer;
  text-align: center;
  padding: 0;
  width: 100%;
}

.action-link:hover {
  color: #ff5000;
}

@media (max-width: 992px) {
  .item-row {
    flex-wrap: wrap;
  }
  
  .item-info {
    width: calc(100% - 120px);
  }
  
  .item-price-col,
  .item-quantity-col,
  .item-actions-col {
    margin-top: 12px;
  }
}
</style>