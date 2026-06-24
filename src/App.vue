<template>
  <div class="app">
    <NavBar />
    <HeroSection @search="handleSearch" />
    <FilterTabs @change="handleFilterChange" />
    <section class="food-grid">
      <FoodCard 
        v-for="food in filteredFoods" 
        :key="food.id" 
        :food="food"
        @click="openFoodModal"
      />
    </section>
    <Footer />
    <FoodModal 
      :visible="modalVisible" 
      :food="selectedFood"
      @close="closeFoodModal" 
    />
    <button class="scroll-top-btn" :class="{ show: showScrollTop }" @click="scrollToTop">⬆️</button>
  </div>
</template>

<script>
import { ref, computed } from 'vue'
import NavBar from './components/NavBar.vue'
import HeroSection from './components/HeroSection.vue'
import FilterTabs from './components/FilterTabs.vue'
import FoodCard from './components/FoodCard.vue'
import FoodModal from './components/FoodModal.vue'
import Footer from './components/Footer.vue'

export default {
  name: 'App',
  components: {
    NavBar,
    HeroSection,
    FilterTabs,
    FoodCard,
    FoodModal,
    Footer
  },
  setup() {
    const foods = ref([
      {
        id: 1,
        name: '苗家酸汤',
        description: '苗族传统酸汤，以天然发酵酸汤为底，搭配鲜嫩竹笋和山野药材，酸辣开胃，回味无穷。',
        price: 58,
        unit: '份',
        rating: 4.8,
        image: 'https://neeko-copilot.bytedance.net/api/text_to_image?prompt=Miao%20ethnic%20traditional%20sour%20soup%20with%20bamboo%20shoots%20and%20herbs%20in%20ceramic%20bowl&image_size=landscape_4_3',
        badge: '传统美食',
        category: 'traditional',
        cookTime: '45分钟',
        servings: '2-3人份'
      },
      {
        id: 2,
        name: '苗家糍粑',
        description: '精选优质糯米，手工打制而成，软糯香甜，可蘸蜂蜜或黄豆粉食用，是苗家节庆必备美食。',
        price: 28,
        unit: '份',
        rating: 4.6,
        image: 'https://neeko-copilot.bytedance.net/api/text_to_image?prompt=Miao%20ethnic%20glutinous%20rice%20cake%20with%20red%20beans%20traditional%20dessert&image_size=landscape_4_3',
        badge: '特色小吃',
        category: 'snacks',
        cookTime: '20分钟',
        servings: '2人份'
      },
      {
        id: 3,
        name: '苗家腊肉',
        description: '选用本地土猪肉，经传统工艺腌制烟熏，色泽红亮，肥而不腻，风味独特。',
        price: 68,
        unit: '份',
        rating: 4.9,
        image: 'https://neeko-copilot.bytedance.net/api/text_to_image?prompt=Miao%20ethnic%20braised%20pork%20with%20bamboo%20shoots%20traditional%20Chinese%20cuisine&image_size=landscape_4_3',
        badge: '招牌菜',
        category: 'traditional',
        cookTime: '即食',
        servings: '2人份'
      },
      {
        id: 4,
        name: '苗家米酒',
        description: '采用山泉水和优质糯米发酵而成，酒香浓郁，口感醇厚，是苗家待客佳品。',
        price: 48,
        unit: '壶',
        rating: 4.7,
        image: 'https://neeko-copilot.bytedance.net/api/text_to_image?prompt=Miao%20ethnic%20rice%20wine%20in%20ceramic%20jar%20traditional%20fermented%20beverage&image_size=landscape_4_3',
        badge: '特色饮品',
        category: 'desserts',
        cookTime: '发酵30天',
        servings: '500ml'
      },
      {
        id: 5,
        name: '雷公山野菜',
        description: '采自雷公山深处的新鲜野菜，清炒或凉拌，口感爽脆，营养丰富，充满山野气息。',
        price: 38,
        unit: '份',
        rating: 4.5,
        image: 'https://neeko-copilot.bytedance.net/api/text_to_image?prompt=Wild%20vegetables%20from%20Leigong%20Mountain%20stir%20fried%20Chinese%20cuisine&image_size=landscape_4_3',
        badge: '时令蔬菜',
        category: 'traditional',
        cookTime: '10分钟',
        servings: '2人份'
      },
      {
        id: 6,
        name: '糯米酒汤圆',
        description: '以苗家糯米酒为汤底，搭配手工汤圆，甜香四溢，温暖身心，是冬日暖胃佳品。',
        price: 32,
        unit: '碗',
        rating: 4.4,
        image: 'https://neeko-copilot.bytedance.net/api/text_to_image?prompt=Glutinous%20rice%20wine%20tangyuan%20rice%20balls%20sweet%20soup%20Chinese%20dessert&image_size=landscape_4_3',
        badge: '甜点',
        category: 'desserts',
        cookTime: '15分钟',
        servings: '1人份'
      }
    ])

    const currentFilter = ref('all')
    const searchQuery = ref('')
    const modalVisible = ref(false)
    const selectedFood = ref({})
    const showScrollTop = ref(false)

    const filteredFoods = computed(() => {
      let result = foods.value
      
      if (currentFilter.value !== 'all') {
        result = result.filter(food => food.category === currentFilter.value)
      }
      
      if (searchQuery.value) {
        const query = searchQuery.value.toLowerCase()
        result = result.filter(food => 
          food.name.toLowerCase().includes(query) || 
          food.description.toLowerCase().includes(query)
        )
      }
      
      return result
    })

    const handleFilterChange = (filter) => {
      currentFilter.value = filter
    }

    const handleSearch = (query) => {
      searchQuery.value = query
    }

    const openFoodModal = (food) => {
      selectedFood.value = food
      modalVisible.value = true
    }

    const closeFoodModal = () => {
      modalVisible.value = false
    }

    const scrollToTop = () => {
      window.scrollTo({ top: 0, behavior: 'smooth' })
    }

    window.addEventListener('scroll', () => {
      showScrollTop.value = window.scrollY > 300
    })

    return {
      foods,
      filteredFoods,
      modalVisible,
      selectedFood,
      showScrollTop,
      handleFilterChange,
      handleSearch,
      openFoodModal,
      closeFoodModal,
      scrollToTop
    }
  }
}
</script>

<style scoped>
.app {
  min-height: 100vh;
}

.food-grid {
  max-width: 1200px;
  margin: 0 auto;
  padding: 2rem;
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
  gap: 2rem;
}

.scroll-top-btn {
  position: fixed;
  bottom: 2rem;
  right: 2rem;
  width: 50px;
  height: 50px;
  background: linear-gradient(135deg, var(--primary-color) 0%, var(--secondary-color) 100%);
  border: none;
  border-radius: 50%;
  color: var(--accent-color);
  cursor: pointer;
  box-shadow: 0 4px 15px rgba(26, 54, 93, 0.4);
  font-size: 1.2rem;
  transition: all 0.3s ease;
  opacity: 0;
  visibility: hidden;
  z-index: 100;
}

.scroll-top-btn.show {
  opacity: 1;
  visibility: visible;
}

.scroll-top-btn:hover {
  transform: translateY(-3px);
  box-shadow: 0 6px 20px rgba(26, 54, 93, 0.5);
}

@media (max-width: 768px) {
  .food-grid {
    grid-template-columns: 1fr;
    padding: 1rem;
  }
}
</style>