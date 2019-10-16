<template>
  <div id="app">
    <inputGroup/>
  </div>
</template>

<script>
import inputGroup from "./components/input-group.vue";

export default {
  name: "App",
  components: { inputGroup }
};
</script>

<style>
#app {
  font-family: "Roboto";
}
</style>
