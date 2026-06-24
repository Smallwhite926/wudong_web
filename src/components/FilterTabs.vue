<template>
  <section class="filter-section">
    <div class="filter-tabs">
      <button 
        v-for="tab in tabs" 
        :key="tab.id"
        :class="{ active: currentTab === tab.id }"
        @click="setTab(tab.id)"
        class="filter-tab"
      >
        {{ tab.name }}
      </button>
    </div>
  </section>
</template>

<script>
import { ref } from 'vue'

export default {
  name: 'FilterTabs',
  emits: ['change'],
  setup(props, { emit }) {
    const currentTab = ref('all')
    
    const tabs = [
      { id: 'all', name: '全部美食' },
      { id: 'traditional', name: '传统菜肴' },
      { id: 'snacks', name: '特色小吃' },
      { id: 'desserts', name: '甜点饮品' },
      { id: 'restaurants', name: '餐厅推荐' }
    ]
    
    const setTab = (tabId) => {
      currentTab.value = tabId
      emit('change', tabId)
    }
    
    return {
      tabs,
      currentTab,
      setTab
    }
  }
}
</script>

<style scoped>
.filter-section {
  padding: 2rem;
  background: var(--bg-light);
}

.filter-tabs {
  display: flex;
  gap: 1rem;
  flex-wrap: wrap;
  justify-content: center;
  max-width: 1200px;
  margin: 0 auto;
}

.filter-tab {
  padding: 0.7rem 1.5rem;
  border-radius: 25px;
  border: 2px solid var(--primary-color);
  background: transparent;
  color: var(--primary-color);
  cursor: pointer;
  transition: all 0.3s ease;
  font-weight: 500;
  position: relative;
  font-size: 0.95rem;
}

.filter-tab::before,
.filter-tab::after {
  content: '◆';
  position: absolute;
  font-size: 0.6rem;
}

.filter-tab::before {
  left: 8px;
}

.filter-tab::after {
  right: 8px;
}

.filter-tab:hover {
  background: var(--primary-color);
  color: var(--accent-color);
  transform: translateY(-2px);
}

.filter-tab.active {
  background: var(--primary-color);
  color: var(--accent-color);
  box-shadow: 0 4px 12px rgba(26, 54, 93, 0.4);
}

@media (max-width: 768px) {
  .filter-tab {
    padding: 0.6rem 1rem;
    font-size: 0.85rem;
  }
}
</style>