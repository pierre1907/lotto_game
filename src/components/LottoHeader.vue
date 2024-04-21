<template>
  <header class="header">
    <div class="header__content">
      <div class="header__logo">
        <img src="@/assets/logo.png" alt="logo" />
      </div>
      <div class="header__title">
        <h1>Lotto Generator</h1>
      </div>

    </div>
  </header>
</template>

<script>
export default {
  name: 'LottoHeader',
};
</script>

<style scoped>
.header {
  /*background-color: #f0f0f0;*/
  padding: 20px;
}

.header__content {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.header__logo img {
  width: 80px;
  height: auto;
}

.header__title h1 {
  font-size: 24px;
  margin: 0; /* Reset margin */
  color: #333;
}
</style>
