<template>
  <div>
    <input v-model="query" placeholder="Enter city name" @input="searchLocation" />
    <ul v-if="locations.length">
      <li v-for="location in locations" :key="location.id" @click="selectLocation(location)">
        {{ location.name }} ({{ location.country }})
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      query: '',
      locations: [],
    };
  },
  methods: {
    async searchLocation() {
      if (this.query.length > 2) {
        const apiUrl = `https://geocoding-api.open-meteo.com/v1/search?name=${this.query}&count=10&language=en&format=json`;
        const response = await fetch(apiUrl);
        const data = await response.json();
        this.locations = data.results;
      }
    },
    selectLocation(location) {
      this.$emit('selectLocation', location);
    },
  },
};
</script>

<style scoped>
/* Стили для поиска */
input {
  padding: 10px;
  margin-bottom: 10px;
}
</style>
