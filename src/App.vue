<template>
  <div id="app">
    <HRapp/>
  </div>
</template>

<script>
import HRapp from "./components/HR-App.vue";

export default {
  name: "app",
  components: {
    HRapp
  }
};
</script>

<style lang="scss">
#app {
  font-family: "Roboto", Helvetica, Arial, sans-serif;
  color: #2c3e50;
}
</style>
