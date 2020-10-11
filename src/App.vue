<template>
  <div id="app">
    <RegistrationForm />

  </div>
</template>

<script>
import RegistrationForm from './components/RegistrationForm.vue';

export default {
  name: 'App',
  components: {
    RegistrationForm,
  },
};
</script>

<style lang="scss">
@import 'assets/style/App.sass';
</style>
