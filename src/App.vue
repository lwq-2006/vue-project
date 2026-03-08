<script setup>
import { ref, computed } from 'vue'
import CartHeader from './components/CartHeader.vue'
import CartTabs from './components/CartTabs.vue'
import CartToolbar from './components/CartToolbar.vue'
import CouponBanner from './components/CouponBanner.vue'
import ShopSection from './components/ShopSection.vue'
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
        couponPrice: 75.9,
        quantity: 1,
        checked: true,
        tags: ['官方正品', '不支持7天无理由退货', '极速退款'],
        image: '/vue-dist/assets/DIMOO.png'
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
        couponPrice: 103.67,
        quantity: 1,
        checked: true,
        tags: ['官方立减15元', '3期免息', '淘金币抵'],
        image: '/vue-dist/assets/蜡笔小新小夜灯.png'
      }
    ]
  },
  {
    id: 3,
    shop: '芙泊颜旗舰店',
    shopChecked: false,
    platform: '天猫',
    items: [
      {
        id: 301,
        name: '【大眼睛与小眼睛】来袭限定三层整妆粉底液妆前乳粉饼套组',
        spec: '颜色分类: P01粉调最白',
        price: 29.9,
        originalPrice: 99.9,
        couponPrice: 29.9,
        quantity: 1,
        checked: false,
        tags: ['首单立减2元', '消费券', '退货险', '15天价保'],
        image: '/vue-dist/assets/熊猫粉饼.png'
      }
    ]
  },
  {
    id: 4,
    shop: '小柴柴的杂货铺',
    shopChecked: false,
    platform: '淘宝',
    items: [
      {
        id: 401,
        name: '超级立新 新款笔袋小简约创意可爱少女心ins潮铅笔盒大容量文具袋',
        spec: '颜色分类: 蜡笔小新',
        price: 3.4,
        originalPrice: 3.9,
        couponPrice: 3.4,
        quantity: 1,
        checked: false,
        tags: ['超级立新0.39元', '淘金币', '7天价保'],
        image: '/vue-dist/assets/蜡笔小新创可贴.png'
      }
    ]
  },
  {
    id: 5,
    shop: '琦花旗舰店',
    shopChecked: false,
    platform: '天猫',
    items: [
      {
        id: 501,
        name: '38焕新周 法式减龄职业衬衫女新款春夏内搭薄款面试衬衣设计感小众',
        spec: '尺码: S',
        price: 78.5,
        originalPrice: 87,
        couponPrice: 78.5,
        quantity: 1,
        checked: false,
        tags: ['信用卡支付', '官方立减0.5元', '3期免息', '退货险'],
        image: '/vue-dist/assets/衬衫.png'
      }
    ]
  },
  {
    id: 6,
    shop: '慕茵旗舰店',
    shopChecked: false,
    platform: '天猫',
    items: [
      {
        id: 601,
        name: '超级立新 甜美黄色小刺猬条纹衬衫女大学生2025春夏新款宽松bf风',
        spec: '尺码: S',
        price: 31.2,
        originalPrice: 45.8,
        couponPrice: 31.2,
        quantity: 1,
        checked: false,
        tags: ['超级立新4.6元', '退货险', '7天价保'],
        image: '/vue-dist/assets/黄色小狗开衫.png'
      }
    ]
  },
  {
    id: 7,
    shop: 'AONW',
    shopChecked: false,
    platform: '淘宝',
    items: [
      {
        id: 701,
        name: '38焕新周 AONW美式涂鸦印花连帽卫衣女秋冬新款加绒宽松',
        spec: '尺码: S',
        price: 121,
        originalPrice: 138,
        couponPrice: 121,
        quantity: 1,
        checked: false,
        tags: ['消费券', '官方立减17元', '大促价保'],
        image: '/vue-dist/assets/连帽卫衣.png'
      }
    ]
  },
  {
    id: 8,
    shop: '莹玥原创工作室',
    shopChecked: false,
    platform: '淘宝',
    items: [
      {
        id: 801,
        name: '38焕新周 韩系休闲运动套装女春秋季学院风宽松拼色外套',
        spec: '尺码: S',
        price: 120.67,
        originalPrice: 138,
        couponPrice: 120.67,
        quantity: 1,
        checked: false,
        tags: ['消费券', '官方立减17元', '12期免息'],
        image: '/vue-dist/assets/运动服套装.png'
      }
    ]
  },
  {
    id: 9,
    shop: 'JEEPSPIRIT 品牌店',
    shopChecked: false,
    platform: '淘宝',
    items: [
      {
        id: 901,
        name: 'JEEP美式条纹外套女2026新款小个子早秋立领韩版学院风运动',
        spec: '尺码: S',
        price: 99,
        originalPrice: 124,
        couponPrice: 99,
        quantity: 1,
        checked: false,
        tags: ['直降25元', '大促价保', '7天无理由'],
        image: '/vue-dist/assets/条纹外套.png'
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

const cartItemCount = computed(() => {
  return cartItems.value.reduce((total, shop) => {
    return total + shop.items.reduce((shopTotal, item) => {
      return shopTotal + item.quantity
    }, 0)
  }, 0)
})

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
  { 
    id: 1, 
    name: '泡泡玛特DIMOO限定盲盒新品榜·第2名', 
    price: 79, 
    image: '/vue-dist/assets/DIMOO2.png',
    platform: 'tmall',
    promoTags: [],
    sales: '1万+人购买'
  },
  { 
    id: 2, 
    name: 'DUSK三条杠双面穿夹克女春秋韩版宽松休闲外套', 
    price: 116.01, 
    image: '/vue-dist/assets/条纹外套.png',
    platform: 'tmall',
    promoTags: ['超级立减17.43元', '退货宝'],
    sales: '1000+人购买'
  },
  { 
    id: 3, 
    name: '正版联名蜡笔小新生日礼物送女生闺蜜创意礼盒', 
    price: 138, 
    image: '/vue-dist/assets/蜡笔大礼物.png',
    platform: 'tmall',
    promoTags: ['38焕新周', '大促价保', '退货宝'],
    sales: '200+人购买'
  },
  { 
    id: 4, 
    name: '【学院风减龄穿搭】休闲运动套装女春秋2024新款', 
    price: 121, 
    image: '/vue-dist/assets/套装衣服.png',
    platform: 'tmall',
    promoTags: ['38焕新周', '官方立减12%'],
    sales: '41人购买'
  },
  { 
    id: 5, 
    name: '微胖MM蓝色收腰绑带长袖衬衫女春季新款显瘦上衣', 
    price: 55.8, 
    image: '/vue-dist/assets/衬衫2.png',
    platform: 'tmall',
    promoTags: ['超级立减10%', '退货宝', '包邮'],
    sales: '8人购买'
  },
  { 
    id: 6, 
    name: '美式复古小狗刺绣宽松休闲卫衣女春秋薄款外套', 
    price: 52.7, 
    image: '/vue-dist/assets/小狗外套.png',
    platform: 'tmall',
    promoTags: ['38焕新周', '官方立减12%'],
    sales: '1000+人购买'
  },
  { 
    id: 7, 
    name: '美诺萌兰蜜粉饼定妆散粉控油持久遮瑕防水防汗', 
    price: 32.9, 
    image: '/vue-dist/assets/熊猫粉饼.png',
    platform: 'tmall',
    promoTags: ['入选百亿补贴定妆粉好评榜'],
    sales: '500+人购买'
  },
  { 
    id: 8, 
    name: '【无畏契约系列】坐姿小摆件游戏周边手办模型', 
    price: 33.9, 
    image: '/vue-dist/assets/DIMOO.png',
    platform: 'tmall',
    promoTags: [],
    sales: '1000+人购买'
  },
  { 
    id: 6, 
    name: '泡泡玛特DIMOO如果今天星满29减3', 
    price: 20, 
    image: '/vue-dist/assets/DIMOO3.png',
    platform: 'tmall',
    promoTags: ['满29减3'],
    sales: '500+人购买'
  },
  { 
    id: 7, 
    name: '条纹开衫外套女新款美式', 
    price: 69, 
    image: '/vue-dist/assets/开衫外套.png',
    platform: 'tmall',
    promoTags: ['38焕新周', '官方立减15%'],
    sales: '100+人购买'
  },
  { 
    id: 8, 
    name: '蜡笔小新玩偶花束卡通花', 
    price: 43.9, 
    image: '/vue-dist/assets/蜡笔花束.png',
    platform: 'tmall',
    promoTags: ['38焕新周', '官方立减12%'],
    sales: '1000+人购买'
  },
  { 
    id: 9, 
    name: '【学院风穿搭】休闲运动', 
    price: 103, 
    image: '/vue-dist/assets/运动服套装.png',
    platform: 'tmall',
    promoTags: ['38焕新周', '官方立减12%'],
    sales: '500+人购买'
  },
  { 
    id: 10, 
    name: '韩系穿搭趣味小狗刺绣条纹衬', 
    price: 57.66, 
    image: '/vue-dist/assets/黄色外套.png',
    platform: 'tmall',
    promoTags: ['官方立减12%', '退货宝', '包邮'],
    sales: '8人购买'
  },
  { 
    id: 11, 
    name: '十字满印字母卫衣女秋冬', 
    price: 61.5, 
    image: '/vue-dist/assets/十字卫衣.png',
    platform: 'tmall',
    promoTags: ['38焕新周', '官方立减12%'],
    sales: '200+人购买'
  },
  { 
    id: 12, 
    name: '蜡笔小新联名2025新款', 
    price: 109.65, 
    image: '/vue-dist/assets/蜡笔手表.png',
    platform: 'tmall',
    promoTags: ['入选圆形儿童腕表热卖榜'],
    sales: '500+人购买'
  }
])
</script>

<template>
  <div class="taobao-cart">
    <CartHeader :cartItemCount="cartItemCount" />
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

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', 'PingFang SC', 'Hiragino Sans GB', 'Microsoft YaHei', sans-serif;
  background-color: white;
}
</style>

<style scoped>
.taobao-cart {
  min-height: 100vh;
  background-color: white;
}

.main {
  min-width: 780px;
  padding-left: 64px;
  padding-right: 64px;
  margin: auto;
  max-width: 1680px;
  padding-left: 80px;
  padding-right: 80px;
  position: relative;
  padding: 0 0 20px 0;
  padding-right: 360px;
}

.content-wrapper {
  width: 100%;
}

.cart-container {
  background-color: white;
  border-radius: 8px;
  padding: 0 24px 24px 0;
}

.cart-list {
  padding-top: 8px;
}

@media (max-width: 1200px) {
  .main {
    padding-right: 20px;
    max-width: 100%;
  }
}

@media (max-width: 768px) {
  .main {
    padding: 10px;
  }
  
  .cart-container {
    padding: 0 16px 16px;
    border-radius: 4px;
  }
}
</style>