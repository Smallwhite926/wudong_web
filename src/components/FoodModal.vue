<template>
  <div v-if="visible" class="modal-overlay" @click="handleOverlayClick">
    <div class="modal" @click.stop>
      <div class="modal-header">
        <h2 class="modal-title">{{ food.name }}</h2>
        <button class="modal-close" @click="handleClose">×</button>
      </div>
      <div class="modal-body">
        <img :src="food.image" :alt="food.name" class="modal-food-image">
        <div class="modal-food-info">
          <h3>菜品介绍</h3>
          <p>{{ food.description }}</p>
        </div>
        <div class="modal-food-details">
          <div class="detail-item">
            <span class="detail-label">价格</span>
            <span class="detail-value">¥{{ food.price }}/{{ food.unit }}</span>
          </div>
          <div class="detail-item">
            <span class="detail-label">评分</span>
            <span class="detail-value">⭐ {{ food.rating }}</span>
          </div>
          <div class="detail-item">
            <span class="detail-label">烹饪时间</span>
            <span class="detail-value">{{ food.cookTime }}</span>
          </div>
          <div class="detail-item">
            <span class="detail-label">份量</span>
            <span class="detail-value">{{ food.servings }}</span>
          </div>
        </div>
        <div class="modal-actions">
          <button class="btn-secondary" @click="handleClose">关闭</button>
          <button class="btn-primary">立即预订</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'FoodModal',
  props: {
    visible: {
      type: Boolean,
      default: false
    },
    food: {
      type: Object,
      default: () => ({})
    }
  },
  emits: ['close'],
  setup(props, { emit }) {
    const handleClose = () => {
      emit('close')
    }
    
    const handleOverlayClick = () => {
      emit('close')
    }
    
    return {
      handleClose,
      handleOverlayClick
    }
  }
}
</script>

<style scoped>
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.6);
  z-index: 1000;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 1rem;
  animation: fadeIn 0.3s ease;
}

@keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}

.modal {
  background: white;
  border-radius: 15px;
  max-width: 600px;
  width: 100%;
  max-height: 90vh;
  overflow-y: auto;
  box-shadow: 0 20px 50px rgba(0, 0, 0, 0.3);
  animation: slideUp 0.3s ease;
}

@keyframes slideUp {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.modal-header {
  background: linear-gradient(135deg, var(--primary-color) 0%, var(--primary-dark) 100%);
  padding: 1.5rem;
  color: var(--text-light);
  display: flex;
  justify-content: space-between;
  align-items: center;
  border-radius: 15px 15px 0 0;
  position: sticky;
  top: 0;
}

.modal-title {
  font-size: 1.3rem;
  font-weight: bold;
  color: var(--accent-color);
}

.modal-close {
  background: rgba(255, 255, 255, 0.2);
  border: none;
  color: var(--text-light);
  width: 35px;
  height: 35px;
  border-radius: 50%;
  cursor: pointer;
  font-size: 1.2rem;
  transition: all 0.3s ease;
  display: flex;
  align-items: center;
  justify-content: center;
}

.modal-close:hover {
  background: rgba(255, 255, 255, 0.3);
}

.modal-body {
  padding: 1.5rem;
}

.modal-food-image {
  width: 100%;
  height: 250px;
  object-fit: cover;
  border-radius: 10px;
  margin-bottom: 1.5rem;
}

.modal-food-info {
  margin-bottom: 1rem;
}

.modal-food-info h3 {
  color: var(--primary-color);
  margin-bottom: 0.5rem;
  font-size: 1.1rem;
}

.modal-food-info p {
  color: var(--text-secondary);
  line-height: 1.6;
}

.modal-food-details {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 1rem;
  margin-bottom: 1.5rem;
  padding: 1rem;
  background: var(--bg-light);
  border-radius: 10px;
}

.detail-item {
  display: flex;
  flex-direction: column;
  gap: 0.3rem;
}

.detail-label {
  font-size: 0.85rem;
  color: var(--text-secondary);
}

.detail-value {
  font-weight: 600;
  color: var(--primary-color);
}

.modal-actions {
  display: flex;
  gap: 1rem;
}

.btn-secondary {
  flex: 1;
  padding: 0.8rem;
  border: 2px solid var(--primary-color);
  border-radius: 8px;
  background: transparent;
  color: var(--primary-color);
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s ease;
}

.btn-secondary:hover {
  background: var(--primary-color);
  color: var(--accent-color);
}

.btn-primary {
  flex: 2;
  padding: 0.8rem;
  border: none;
  border-radius: 8px;
  background: linear-gradient(135deg, var(--primary-color) 0%, var(--secondary-color) 100%);
  color: var(--accent-color);
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s ease;
}

.btn-primary:hover {
  box-shadow: 0 4px 12px rgba(26, 54, 93, 0.4);
  transform: translateY(-2px);
}

@media (max-width: 768px) {
  .modal-food-details {
    grid-template-columns: 1fr;
  }
  
  .modal-actions {
    flex-direction: column;
  }
  
  .modal-food-image {
    height: 200px;
  }
}
</style>