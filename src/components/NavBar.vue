<template>
  <nav class="navbar">
    <div class="navbar-container">
      <div class="navbar-logo">
        <div class="logo-icon">🍽️</div>
        <span class="logo-text">乌东文旅</span>
      </div>
      <ul class="navbar-links">
        <li v-for="item in navItems" :key="item.name">
          <a 
            href="#" 
            :class="{ active: currentActive === item.name }"
            @click.prevent="setActive(item.name)"
          >
            {{ item.name }}
          </a>
        </li>
      </ul>
    </div>
  </nav>
</template>

<script>
import { ref } from 'vue'

export default {
  name: 'NavBar',
  setup() {
    const currentActive = ref('首页')
    
    const navItems = [
      { name: '首页' },
      { name: '美食' },
      { name: '景点' },
      { name: '住宿' },
      { name: '联系我们' }
    ]
    
    const setActive = (name) => {
      currentActive.value = name
    }
    
    return {
      navItems,
      currentActive,
      setActive
    }
  }
}
</script>

<style scoped>
.navbar {
  background: linear-gradient(180deg, var(--primary-color) 0%, var(--primary-dark) 100%);
  padding: 1rem 2rem;
  position: sticky;
  top: 0;
  z-index: 100;
  box-shadow: 0 4px 15px rgba(13, 27, 42, 0.4);
}

.navbar-container {
  max-width: 1200px;
  margin: 0 auto;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.navbar-logo {
  display: flex;
  align-items: center;
  gap: 0.8rem;
}

.logo-icon {
  width: 45px;
  height: 45px;
  background: linear-gradient(135deg, var(--accent-color) 0%, #b8955c 100%);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 1.5rem;
  box-shadow: 0 3px 10px rgba(201, 169, 98, 0.5);
}

.logo-text {
  color: var(--accent-color);
  font-size: 1.5rem;
  font-weight: bold;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
}

.navbar-links {
  display: flex;
  gap: 2rem;
  list-style: none;
}

.navbar-links a {
  color: var(--text-light);
  text-decoration: none;
  font-weight: 500;
  padding-bottom: 0.3rem;
  position: relative;
  transition: color 0.3s ease;
}

.navbar-links a:hover {
  color: var(--accent-color);
}

.navbar-links a::after {
  content: '';
  position: absolute;
  bottom: 0;
  left: 50%;
  transform: translateX(-50%);
  width: 0;
  height: 3px;
  background: var(--accent-color);
  transition: width 0.3s ease;
}

.navbar-links a:hover::after,
.navbar-links a.active::after {
  width: 100%;
}

.navbar-links a.active {
  color: var(--accent-color);
}

@media (max-width: 768px) {
  .navbar-links {
    display: none;
  }
}
</style>