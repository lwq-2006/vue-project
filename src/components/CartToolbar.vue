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
      <div class="select-all">
        <input type="checkbox" :checked="selectAll" @change="handleToggleSelectAll" id="toolbarSelectAll" />
        <label for="toolbarSelectAll">全选</label>
      </div>
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
        <input type="text" class="search-input" placeholder="搜索购物车商品" />
        <span class="search-icon">🔍</span>
      </div>
    </div>
  </div>
</template>

<style scoped>
.cart-toolbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 12px 0;
}

.toolbar-left {
  display: flex;
  align-items: center;
  gap: 20px;
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

.toolbar-btn {
  background: none;
  border: none;
  color: #666;
  font-size: 14px;
  cursor: pointer;
}

.toolbar-btn:hover {
  color: #ff5000;
}

.delete-btn:hover {
  color: #ff0000;
}

.toolbar-right {
  display: flex;
  align-items: center;
  gap: 12px;
}

.toolbar-select {
  padding: 6px 12px;
  border: 1px solid #ddd;
  border-radius: 4px;
  font-size: 12px;
  color: #666;
  background: white;
  cursor: pointer;
}

.search-box {
  position: relative;
  display: flex;
  align-items: center;
}

.search-input {
  width: 200px;
  padding: 8px 32px 8px 12px;
  border: 1px solid #ddd;
  border-radius: 4px;
  font-size: 12px;
  outline: none;
}

.search-input:focus {
  border-color: #ff5000;
}

.search-icon {
  position: absolute;
  right: 10px;
  font-size: 14px;
  color: #999;
}
</style>
