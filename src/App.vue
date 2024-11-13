<template>
  <div id="app">
    <h1>Weather App</h1>
    <Weather />
  </div>
</template>

<script>
import Weather from "./components/Weather.vue";

export default {
  components: {
    Weather,
  },
};
</script>

<style>
/* Add some basic styling */
body {
  font-family: Arial, sans-serif;
  text-align: center;
  background: #f5f5f5;
  color: #262626 !important;
}
</style>
