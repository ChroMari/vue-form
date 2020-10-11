<template>
  <div class="modal">
    <div class="sa-icon sa-info"></div>
    <h2 class="modal__title">Клиент создан!</h2>
    <p class="modal__text">Ваши данные добавлены. Спасибо за регистрацию.</p>
  </div>
</template>

<script>
export default {
  name: 'RegistrationPopup',
  data() {
    return {}
  }
};
</script>

<style scoped lang="scss">
  @import '../assets/style/RegistrationPopup.sass';
</style>