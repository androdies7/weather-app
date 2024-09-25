<template>
  <div v-if="forecast">
    <h3>Weather Forecast:</h3>
    <ul>
      <li v-for="(temp, index) in forecast" :key="index">
        Hour {{ index }}: {{ temp }}°C
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  props: {
    forecast: Array,
  },
};
</script>

<style scoped>
/* Стили для отображения прогноза */
ul {
  list-style: none;
  padding: 0;
}

li {
  padding: 5px 0;
}
</style>
