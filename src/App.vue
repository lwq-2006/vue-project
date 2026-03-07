<script setup>
import { ref, computed } from 'vue'
import CartHeader from './components/CartHeader.vue'
import CartTabs from './components/CartTabs.vue'
import CartToolbar from './components/CartToolbar.vue'
import CouponBanner from './components/CouponBanner.vue'
import ShopSection from './components/ShopSection.vue'
import CartFooter from './components/CartFooter.vue'
import RecommendSection from './components/RecommendSection.vue'
import RightSidebar from './components/RightSidebar.vue'

const cartItems = ref([
  {
    id: 1,
    shop: 'TOP DOLL 俱乐部',
    shopChecked: true,
    platform: '淘宝',
    items: [
      {
        id: 101,
        name: 'POPMART泡泡玛特DIMMO如果今天星期几系列手办植绒盲盒潮玩',
        spec: '款式描述: 单个盲盒【全新未拆 概率隐藏】',
        price: 75.9,
        originalPrice: 0,
        quantity: 1,
        checked: true,
        tags: ['官方正品', '不支持7天无理由退货', '极速退款'],
        image: 'https://img.alicdn.com/imgextra/i1/O1CN01eKXZ1L1z3z3z3z3z3_!!6000000006230-0-tbvideo.jpg'
      }
    ]
  },
  {
    id: 2,
    shop: '潮玩手办基地',
    shopChecked: true,
    platform: '淘宝',
    items: [
      {
        id: 201,
        name: '发光校服小新大大号蜡笔小新颜色可选手办潮玩摆件小夜灯生日礼物',
        spec: '颜色分类: 中号发光校服小新【25cm高】充电款+彩盒包装',
        price: 103.67,
        originalPrice: 119,
        quantity: 1,
        checked: true,
        tags: ['官方立减15元', '3期免息', '淘金币抵'],
        image: 'https://img.alicdn.com/imgextra/i2/O1CN01fYfZ1L1z3z3z3z3z3_!!6000000006230-0-tbvideo.jpg'
      }
    ]
  },
  {
    id: 3,
    shop: '美诺旗舰店',
    shopChecked: false,
    platform: '天猫',
    items: [
      {
        id: 301,
        name: '美诺粉饼控油定妆持久遮瑕蜜粉散粉补妆防水防汗不脱妆',
        spec: '颜色分类: 01#透明色【适合白皙/自然肤色】',
        price: 39.9,
        originalPrice: 79.9,
        quantity: 1,
        checked: false,
        tags: ['天猫', '正品保障', '运费险'],
        image: 'https://img.alicdn.com/imgextra/i4/O1CN01hZfZ1L1z3z3z3z3z3_!!6000000006230-0-tbvideo.jpg'
      }
    ]
  }
])

const selectAll = ref(false)

const toggleSelectAll = () => {
  selectAll.value = !selectAll.value
  cartItems.value.forEach(shop => {
    shop.shopChecked = selectAll.value
    shop.items.forEach(item => {
      item.checked = selectAll.value
    })
  })
}

const toggleShopCheck = (shop) => {
  shop.shopChecked = !shop.shopChecked
  shop.items.forEach(item => {
    item.checked = shop.shopChecked
  })
  updateSelectAll()
}

const toggleItemCheck = (shop, item) => {
  item.checked = !item.checked
  shop.shopChecked = shop.items.every(i => i.checked)
  updateSelectAll()
}

const updateSelectAll = () => {
  const allItems = cartItems.value.flatMap(shop => shop.items)
  selectAll.value = allItems.length > 0 && allItems.every(item => item.checked)
}

const decreaseQuantity = (item) => {
  if (item.quantity > 1) {
    item.quantity--
  }
}

const increaseQuantity = (item) => {
  item.quantity++
}

const deleteItem = (shop, item) => {
  const itemIndex = shop.items.findIndex(i => i.id === item.id)
  if (itemIndex !== -1) {
    shop.items.splice(itemIndex, 1)
    if (shop.items.length === 0) {
      const shopIndex = cartItems.value.findIndex(s => s.id === shop.id)
      if (shopIndex !== -1) {
        cartItems.value.splice(shopIndex, 1)
      }
    }
  }
  updateSelectAll()
}

const totalPrice = computed(() => {
  let total = 0
  cartItems.value.forEach(shop => {
    shop.items.forEach(item => {
      if (item.checked) {
        total += item.price * item.quantity
      }
    })
  })
  return total.toFixed(2)
})

const selectedCount = computed(() => {
  let count = 0
  cartItems.value.forEach(shop => {
    shop.items.forEach(item => {
      if (item.checked) {
        count++
      }
    })
  })
  return count
})

const recommendItems = ref([
  { id: 1, name: '蜡笔小新 正版授权 可爱毛绒公仔', price: 29.9, image: 'https://img.alicdn.com/imgextra/i1/O1CN01jZfZ1L1z3z3z3z3z3_!!6000000006230-0-tbvideo.jpg' },
  { id: 2, name: '数字油画 diy手绘填充 减压装饰画', price: 48.8, image: 'https://img.alicdn.com/imgextra/i2/O1CN01kZfZ1L1z3z3z3z3z3_!!6000000006230-0-tbvideo.jpg' },
  { id: 3, name: '敦煌研究院 文创手办摆件 可爱神兽', price: 89, image: 'https://img.alicdn.com/imgextra/i3/O1CN01lZfZ1L1z3z3z3z3z3_!!6000000006230-0-tbvideo.jpg' },
  { id: 4, name: '粉色卡通鼠标垫 可爱女生办公桌垫', price: 19.9, image: 'https://img.alicdn.com/imgextra/i4/O1CN01mZfZ1L1z3z3z3z3z3_!!6000000006230-0-tbvideo.jpg' },
  { id: 5, name: '水乳套装 补水保湿 护肤品礼盒', price: 168, image: 'https://img.alicdn.com/imgextra/i5/O1CN01nZfZ1L1z3z3z3z3z3_!!6000000006230-0-tbvideo.jpg' },
  { id: 6, name: '春秋新款女装 时尚休闲外套', price: 259, image: 'https://img.alicdn.com/imgextra/i6/O1CN01oZfZ1L1z3z3z3z3z3_!!6000000006230-0-tbvideo.jpg' },
  { id: 7, name: '百搭休闲裤 显瘦显高 垂感好', price: 129, image: 'https://img.alicdn.com/imgextra/i7/O1CN01pZfZ1L1z3z3z3z3z3_!!6000000006230-0-tbvideo.jpg' },
  { id: 8, name: '法式连衣裙 优雅气质 收腰显瘦', price: 299, image: 'https://img.alicdn.com/imgextra/i8/O1CN01qZfZ1L1z3z3z3z3z3_!!6000000006230-0-tbvideo.jpg' }
])
</script>

<template>
  <div class="taobao-cart">
    <CartHeader />
    <main class="main">
      <div class="content-wrapper">
        <div class="cart-container">
          <CartTabs />
          <CartToolbar
            :selectAll="selectAll"
            @toggle-select-all="toggleSelectAll"
          />
          <CouponBanner />
          <div class="cart-list">
            <ShopSection
              v-for="shop in cartItems"
              :key="shop.id"
              :shop="shop"
              @toggle-shop-check="toggleShopCheck"
              @toggle-item-check="toggleItemCheck"
              @decrease-quantity="decreaseQuantity"
              @increase-quantity="increaseQuantity"
              @delete-item="deleteItem"
            />
          </div>
          <CartFooter
            :selectAll="selectAll"
            :selectedCount="selectedCount"
            :totalPrice="totalPrice"
            @toggle-select-all="toggleSelectAll"
          />
        </div>
        <RecommendSection :recommendItems="recommendItems" />
      </div>
    </main>
    <RightSidebar
      :selectedCount="selectedCount"
      :totalPrice="totalPrice"
    />
  </div>
</template>

<style scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.taobao-cart {
  min-height: 100vh;
  background-color: #f5f5f5;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
}

.main {
  max-width: 1200px;
  margin: 0 auto;
  padding: 20px;
  padding-right: 356px;
}

.content-wrapper {
  width: 100%;
}

.cart-container {
  background-color: white;
  border-radius: 4px;
  padding: 0 20px 20px;
}

.cart-list {
  padding-top: 8px;
}

@media (max-width: 1200px) {
  .main {
    padding-right: 20px;
  }
}
</style>
