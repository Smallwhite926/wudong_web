<template>
  <section class="hero-section">
    <div class="hero-pattern"></div>
    <div class="hero-content">
      <h1 class="hero-title">品味乌东 · 美食之旅</h1>
      <p class="hero-subtitle">探索乌东村独特的苗族美食文化，感受淳朴自然的味蕾盛宴</p>
      <div class="search-container">
        <input 
          type="text" 
          class="search-input" 
          v-model="searchQuery"
          placeholder="搜索美食、餐厅..."
          @keyup.enter="handleSearch"
        >
        <button class="search-btn" @click="handleSearch">🔍</button>
      </div>
    </div>
  </section>
</template>

<script>
import { ref } from 'vue'

export default {
  name: 'HeroSection',
  emits: ['search'],
  setup(props, { emit }) {
    const searchQuery = ref('')
    
    const handleSearch = () => {
      emit('search', searchQuery.value)
    }
    
    return {
      searchQuery,
      handleSearch
    }
  }
}
</script>

<style scoped>
.hero-section {
  padding: 4rem 2rem;
  text-align: center;
  position: relative;
  overflow: hidden;
  background: linear-gradient(rgba(26, 54, 93, 0.9), rgba(13, 27, 42, 0.85)), 
              url('data:image/svg+xml,%3Csvg width="40" height="40" viewBox="0 0 40 40" xmlns="http://www.w3.org/2000/svg"%3E%3Cpath d="M0 20L20 0L40 20L20 40Z" fill="%23c9a962" fill-opacity="0.1"/%3E%3C/svg%3E');
}

.hero-pattern {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 60px;
  background: repeating-linear-gradient(
    45deg,
    transparent,
    transparent 10px,
    rgba(201, 169, 98, 0.1) 10px,
    rgba(201, 169, 98, 0.1) 12px
  );
}

.hero-content {
  position: relative;
  z-index: 1;
}

.hero-title {
  font-size: 3rem;
  color: var(--accent-color);
  margin-bottom: 1rem;
  padding-top: 2rem;
  text-shadow: 3px 3px 6px rgba(0, 0, 0, 0.4);
}

.hero-subtitle {
  font-size: 1.2rem;
  color: var(--text-light);
  opacity: 0.9;
  margin-bottom: 2rem;
}

.search-container {
  max-width: 500px;
  margin: 0 auto;
  position: relative;
}

.search-input {
  width: 100%;
  padding: 1rem 2.5rem 1rem 1.5rem;
  border: 2px solid rgba(201, 169, 98, 0.3);
  border-radius: 50px;
  font-size: 1rem;
  background: rgba(255, 255, 255, 0.1);
  color: white;
  transition: all 0.3s ease;
}

.search-input::placeholder {
  color: rgba(255, 255, 255, 0.6);
}

.search-input:focus {
  outline: none;
  border-color: var(--accent-color);
  box-shadow: 0 0 0 3px rgba(201, 169, 98, 0.2);
  transform: translateY(-2px);
}

.search-btn {
  position: absolute;
  right: 5px;
  top: 50%;
  transform: translateY(-50%);
  border: 2px solid var(--accent-color);
  color: var(--accent-color);
  background: transparent;
  width: 40px;
  height: 40px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: all 0.3s ease;
  font-size: 1rem;
}

.search-btn:hover {
  background: var(--accent-color);
  color: var(--primary-color);
  transform: translateY(-50%) scale(1.1);
}

@media (max-width: 768px) {
  .hero-title {
    font-size: 2rem;
  }
  
  .hero-subtitle {
    font-size: 1rem;
  }
}
</style>