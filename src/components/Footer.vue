<template>
  <footer class="footer">
    <div class="footer-content">
      <div class="footer-top">
        <div class="footer-logo">
          <div class="logo-icon">🍽️</div>
          <span class="logo-text">乌东文旅美食</span>
        </div>
        <div class="footer-links">
          <div class="link-group">
            <h4>快速链接</h4>
            <ul>
              <li><a href="#">首页</a></li>
              <li><a href="#">美食</a></li>
              <li><a href="#">景点</a></li>
              <li><a href="#">住宿</a></li>
            </ul>
          </div>
          <div class="link-group">
            <h4>关于我们</h4>
            <ul>
              <li><a href="#">平台介绍</a></li>
              <li><a href="#">联系我们</a></li>
              <li><a href="#">加入我们</a></li>
              <li><a href="#">隐私政策</a></li>
            </ul>
          </div>
          <div class="link-group">
            <h4>联系方式</h4>
            <ul>
              <li>📍 贵州省黔东南州乌东村</li>
              <li>📞 0855-1234567</li>
              <li>📧 info@wudong.com</li>
            </ul>
          </div>
        </div>
      </div>
      <div class="footer-bottom">
        <p>&copy; 2024 乌东文旅美食平台 | 黔ICP备12345678号</p>
      </div>
    </div>
  </footer>
</template>

<script>
export default {
  name: 'Footer'
}
</script>

<style scoped>
.footer {
  background: linear-gradient(180deg, var(--primary-dark) 0%, var(--primary-color) 100%);
  padding: 3rem 2rem;
  margin-top: 2rem;
}

.footer-content {
  max-width: 1200px;
  margin: 0 auto;
}

.footer-top {
  display: flex;
  flex-wrap: wrap;
  gap: 3rem;
  justify-content: space-between;
  padding-bottom: 2rem;
  border-bottom: 1px solid rgba(201, 169, 98, 0.2);
}

.footer-logo {
  display: flex;
  align-items: center;
  gap: 0.8rem;
}

.logo-icon {
  width: 50px;
  height: 50px;
  background: linear-gradient(135deg, var(--accent-color) 0%, #b8955c 100%);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 1.6rem;
}

.logo-text {
  color: var(--accent-color);
  font-size: 1.4rem;
  font-weight: bold;
}

.footer-links {
  display: flex;
  gap: 3rem;
  flex-wrap: wrap;
}

.link-group {
  min-width: 150px;
}

.link-group h4 {
  color: var(--accent-color);
  margin-bottom: 1rem;
  font-size: 1rem;
}

.link-group ul {
  list-style: none;
}

.link-group li {
  margin-bottom: 0.5rem;
}

.link-group a {
  color: var(--text-light);
  text-decoration: none;
  opacity: 0.8;
  transition: opacity 0.3s ease;
  font-size: 0.9rem;
}

.link-group a:hover {
  opacity: 1;
}

.footer-bottom {
  padding-top: 1.5rem;
  text-align: center;
}

.footer-bottom p {
  color: var(--text-light);
  opacity: 0.7;
  font-size: 0.85rem;
}

@media (max-width: 768px) {
  .footer-top {
    flex-direction: column;
    align-items: center;
    text-align: center;
  }
  
  .footer-links {
    justify-content: center;
  }
}
</style>