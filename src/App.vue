<template>
  <div id="app">
    <LocationSearch @selectLocation="getWeather" />
    <WeatherDisplay :forecast="forecast" />
  </div>
</template>

<script>
import LocationSearch from './components/LocationSearch.vue';
import WeatherDisplay from './components/WeatherDisplay.vue';

export default {
  data() {
    return {
      forecast: null,
    };
  },
  methods: {
    async getWeather(location) {
      const lat = location.latitude;
      const lon = location.longitude;
      const apiUrl = `https://api.open-meteo.com/v1/forecast?latitude=${lat}&longitude=${lon}&hourly=temperature_2m`;
      const response = await fetch(apiUrl);
      const data = await response.json();
      this.forecast = data.hourly.temperature_2m;
    },
  },
  components: {
    LocationSearch,
    WeatherDisplay,
  },
};
</script>
