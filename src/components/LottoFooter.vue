<template>
  <footer class="footer">
    <div class="footer__content">
      <span>Développé par </span>
      <a href="https://github.com/pierre1907" class="footer__link">Saint-Pierre KASSI ⚜️</a>
      <span> © 2024</span>
    </div>
  </footer>
</template>

<script>
export default {
  name: 'LottoFooter'
};
</script>

<style scoped>
.footer {
  background-color: #333;
  color: #fff;
  padding: 20px 0;
  text-align: center;
  position: fixed;
  bottom: 0;
  width: 100%;
}

.footer__content {
  font-size: 14px;
}

.footer__link {
  color: #fff;
  text-decoration: none;
}

.footer__link:hover {
  text-decoration: underline;
}
</style>
