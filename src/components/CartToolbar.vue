<script setup>
const props = defineProps({
  selectAll: {
    type: Boolean,
    required: true
  }
})

const emit = defineEmits(['toggleSelectAll', 'batchDelete', 'batchFavorite'])

const handleToggleSelectAll = () => {
  emit('toggleSelectAll')
}

const handleBatchDelete = () => {
  emit('batchDelete')
}

const handleBatchFavorite = () => {
  emit('batchFavorite')
}
</script>

<template>
  <div class="cart-toolbar">
    <div class="toolbar-left">
      <label class="select-all">
        <input type="checkbox" :checked="selectAll" @change="handleToggleSelectAll" />
        <span>全选</span>
      </label>
      <button class="toolbar-btn" @click="handleBatchFavorite">移入收藏</button>
      <button class="toolbar-btn delete-btn" @click="handleBatchDelete">删除</button>
    </div>
    <div class="toolbar-right">
      <select class="toolbar-select">
        <option>分类</option>
      </select>
      <select class="toolbar-select">
        <option>状态</option>
      </select>
      <div class="search-box">
        <input type="text" class="search-input" placeholder="搜索购物车内商品" />
        <button class="search-btn">
          <span class="search-icon">
            <svg viewBox="0 0 24 24" width="22" height="22" fill="currentColor">
              <path d="M15.5 14h-.79l-.28-.27C15.41 12.59 16 11.11 16 9.5 16 5.91 13.09 3 9.5 3S3 5.91 3 9.5 5.91 16 9.5 16c1.61 0 3.09-.59 4.23-1.57l.27.28v.79l5 4.99L20.49 19l-4.99-5zm-6 0C7.01 14 5 11.99 5 9.5S7.01 5 9.5 5 14 7.01 14 9.5 11.99 14 9.5 14z"/>
            </svg>
          </span>
        </button>
      </div>
    </div>
  </div>
</template>

<style scoped>
.cart-toolbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 16px 0;
}

.toolbar-left {
  display: flex;
  align-items: center;
  gap: 12px;
}

.select-all {
  display: flex;
  align-items: center;
  gap: 12px;
  cursor: pointer;
  font-size: 14px;
  color: #000;
}

.select-all input[type="checkbox"] {
  width: 22px;
  height: 22px;
  cursor: pointer;
  border: 1px solid #f9f9f9;
  border-radius: 4px;
  accent-color: #ff5000;
  appearance: auto;
}

.toolbar-btn {
  background: white;
  border: 1px solid #d9d9d9;
  color: #000;
  font-size: 14px;
  cursor: pointer;
  padding: 6px 16px;
  border-radius: 6px;
  transition: all 0.2s;
}

.toolbar-btn:hover {
  background-color: #f5f5f5;
  color: #000;
}

.delete-btn:hover {
  color: #000;
  background-color: #f5f5f5;
}

.toolbar-right {
  display: flex;
  align-items: center;
  gap: 16px;
}

.toolbar-select {
  padding: 6px 28px 6px 12px;
  border: 1.5px solid #d9d9d9;
  border-radius: 6px;
  font-size: 14px;
  color: #999;
  background: white;
  cursor: pointer;
  outline: none;
  transition: all 0.2s;
  min-width: 100px;
}

.toolbar-select:hover {
  border-color: #ff5000;
  color: #ff5000;
}

.search-box {
  position: relative;
  display: flex;
  align-items: center;
}

.search-input {
  width: 220px;
  padding: 6px 40px 6px 12px;
  border: 1.5px solid #d9d9d9;
  border-radius: 6px;
  font-size: 14px;
  outline: none;
  color: #333;
  transition: all 0.2s;
}

.search-input:focus {
  border-color: #ff5000;
}

.search-input::placeholder {
  color: #999;
}

.search-btn {
  position: absolute;
  right: 12px;
  top: 50%;
  transform: translateY(-50%);
  background: none;
  border: none;
  padding: 4px;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
}

.search-icon {
  color: #666;
  display: flex;
  align-items: center;
  justify-content: center;
}

.search-icon svg {
  fill: #666;
}

.search-btn:hover .search-icon svg {
  fill: #ff5000;
}

@media (max-width: 768px) {
  .toolbar-right {
    display: none;
  }
}
</style>