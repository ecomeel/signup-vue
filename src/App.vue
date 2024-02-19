<script setup>
import SignUp from "./components/signUp/SignUp.vue";
</script>

<template>
  <div class="container">
    <h1 class="title">Создание аккаунта</h1>
    <p class="description">
      Поля, помеченные знаком * - являются обязательными
    </p>
    <SignUp />
  </div>
</template>

<style scoped lang="scss">
.title {
  font-size: 30px;
  font-weight: 700;
}
.description {
  margin-top: 10px;
  font-size: 16px;
  color: #7f7f7f;
}
</style>

<!-- #7f7f7f gray color -->
<!-- #4B72C2 lbue color -->
<!-- #3d3d3d border color -->
