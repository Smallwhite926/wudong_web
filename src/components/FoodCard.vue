<template>
  <div class="food-card" @click="handleClick">
    <div class="card-pattern"></div>
    <img :src="food.image" :alt="food.name" class="food-image">
    <div class="food-badge">{{ food.badge }}</div>
    <div class="food-content">
      <h3 class="food-title">{{ food.name }}</h3>
      <p class="food-desc">{{ food.description }}</p>
      <div class="food-meta">
        <div class="food-price">¥{{ food.price }}<span>/{{ food.unit }}</span></div>
        <div class="food-rating">
          <span>⭐</span>
          <span>{{ food.rating }}</span>
        </div>
      </div>
      <button class="view-btn">查看详情</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'FoodCard',
  props: {
    food: {
      type: Object,
      required: true
    }
  },
  emits: ['click'],
  setup(props, { emit }) {
    const handleClick = () => {
      emit('click', props.food)
    }
    
    return {
      handleClick
    }
  }
}
</script>

<style scoped>
.food-card {
  background: white;
  border-radius: 10px;
  overflow: hidden;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
  transition: all 0.3s ease;
  position: relative;
}

.food-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 8px 25px rgba(0, 0, 0, 0.15);
}

.card-pattern {
  height: 40px;
  background: repeating-linear-gradient(
    45deg,
    var(--primary-color),
    var(--primary-color) 10px,
    var(--accent-color) 10px,
    var(--accent-color) 12px
  );
}

.food-image {
  width: 100%;
  height: 180px;
  object-fit: cover;
  transition: transform 0.3s ease;
}

.food-card:hover .food-image {
  transform: scale(1.05);
}

.food-badge {
  position: absolute;
  top: 55px;
  right: 15px;
  background: linear-gradient(135deg, var(--accent-color) 0%, #b8955c 100%);
  color: var(--primary-color);
  padding: 0.3rem 0.8rem;
  border-radius: 20px;
  font-size: 0.8rem;
  font-weight: 600;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.2);
}

.food-content {
  padding: 1.5rem;
}

.food-title {
  font-size: 1.3rem;
  font-weight: bold;
  color: var(--primary-color);
  margin-bottom: 0.5rem;
  display: flex;
  align-items: center;
  gap: 0.5rem;
}

.food-title::before {
  content: '';
  width: 4px;
  height: 18px;
  background: linear-gradient(180deg, var(--accent-color) 0%, #b8955c 100%);
  border-radius: 2px;
}

.food-desc {
  color: var(--text-secondary);
  font-size: 0.9rem;
  margin-bottom: 1rem;
  line-height: 1.5;
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  overflow: hidden;
}

.food-meta {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding-top: 1rem;
  border-top: 1px solid var(--border-color);
}

.food-price {
  font-size: 1.3rem;
  font-weight: bold;
  color: #dc2626;
}

.food-price span {
  font-size: 0.8rem;
  font-weight: normal;
  color: var(--text-secondary);
}

.food-rating {
  display: flex;
  align-items: center;
  gap: 0.3rem;
  color: #f59e0b;
  font-weight: 500;
}

.view-btn {
  width: 100%;
  margin-top: 1rem;
  padding: 0.8rem;
  border: 2px solid var(--primary-color);
  background: var(--primary-color);
  color: var(--accent-color);
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s ease;
  position: relative;
  border-radius: 6px;
  font-size: 0.95rem;
}

.view-btn::before,
.view-btn::after {
  content: '◆';
  position: absolute;
  font-size: 0.6rem;
}

.view-btn::before {
  left: 15px;
}

.view-btn::after {
  right: 15px;
}

.view-btn:hover {
  background: transparent;
  color: var(--primary-color);
}

@media (max-width: 768px) {
  .food-card {
    margin-bottom: 1rem;
  }
}
</style>