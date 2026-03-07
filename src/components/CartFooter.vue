<script setup>
const props = defineProps({
  selectAll: {
    type: Boolean,
    required: true
  },
  selectedCount: {
    type: Number,
    required: true
  },
  totalPrice: {
    type: String,
    required: true
  }
})

const emit = defineEmits(['toggleSelectAll'])

const handleToggleSelectAll = () => {
  emit('toggleSelectAll')
}
</script>

<template>
  <div class="cart-footer">
    <div class="footer-left">
      <div class="select-all">
        <input type="checkbox" :checked="selectAll" @change="handleToggleSelectAll" id="selectAllBottom" />
        <label for="selectAllBottom">全选</label>
      </div>
      <button class="batch-delete">删除选中</button>
    </div>
    <div class="footer-right">
      <div class="selected-info">
        已选择 <span class="selected-count">{{ selectedCount }}</span> 件商品
      </div>
      <div class="total-info">
        <span class="total-label">合计：</span>
        <span class="total-amount">¥{{ totalPrice }}</span>
      </div>
      <button class="checkout-btn" :disabled="selectedCount === 0">结算</button>
    </div>
  </div>
</template>

<style scoped>
.cart-footer {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 16px 20px;
  background-color: #fafafa;
  border-top: 1px solid #eee;
  margin-top: 20px;
  border-radius: 0 0 4px 4px;
}

.footer-left {
  display: flex;
  align-items: center;
  gap: 24px;
}

.select-all {
  display: flex;
  align-items: center;
  gap: 8px;
}

.select-all input[type="checkbox"] {
  width: 18px;
  height: 18px;
  cursor: pointer;
}

.select-all label {
  cursor: pointer;
  user-select: none;
  font-size: 14px;
  color: #333;
}

.batch-delete {
  background: none;
  border: none;
  color: #666;
  font-size: 14px;
  cursor: pointer;
}

.batch-delete:hover {
  color: #ff5000;
}

.footer-right {
  display: flex;
  align-items: center;
  gap: 24px;
}

.selected-info {
  font-size: 14px;
  color: #666;
}

.selected-count {
  color: #ff5000;
  font-weight: bold;
  font-size: 18px;
}

.total-info {
  display: flex;
  align-items: baseline;
  gap: 8px;
}

.total-label {
  font-size: 14px;
  color: #666;
}

.total-amount {
  font-size: 24px;
  font-weight: bold;
  color: #ff5000;
}

.checkout-btn {
  padding: 12px 48px;
  background-color: #ff5000;
  color: white;
  border: none;
  border-radius: 4px;
  font-size: 16px;
  font-weight: bold;
  cursor: pointer;
}

.checkout-btn:hover:not(:disabled) {
  background-color: #ff4400;
}

.checkout-btn:disabled {
  background-color: #ffb380;
  cursor: not-allowed;
}

@media (max-width: 768px) {
  .footer-right {
    gap: 12px;
  }

  .checkout-btn {
    padding: 10px 24px;
  }
}
</style>
