<template>
  <div>
    <input
      type="text"
      v-model="city"
      @keyup.enter="fetchWeather"
      placeholder="Enter city"
    />
    <button @click="fetchWeather">Search</button>
    <div v-if="weather">
      <h2>Weather in {{ weather.name }}</h2>
      <p>Temperature: {{ weather.main.temp }}°C</p>
      <p>Condition: {{ weather.weather[0].description }}</p>
      <p>Humidity: {{ weather.main.humidity }}%</p>
      <p>Wind Speed: {{ weather.wind.speed }} m/s</p>
    </div>
    <div v-else-if="error">
      <p>{{ error }}</p>
    </div>
    <div v-else>
      <p>Loading weather data...</p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      weather: null,
      apiKey: "0c8f27037a6809437b45d7953c146cdf",
      city: "London",
      error: null,
    };
  },
  methods: {
    async fetchWeather() {
      try {
        this.error = null;
        const response = await fetch(
          `https://api.openweathermap.org/data/2.5/weather?q=${this.city}&units=metric&appid=${this.apiKey}`
        );
        if (!response.ok) throw new Error("City not found");
        const data = await response.json();
        this.weather = data;
      } catch (error) {
        this.error = error.message;
      }
    },
  },
};
</script>

<style scoped>
/* Add styling */
input {
  padding: 5px;
  font-size: 1em;
}
button {
  padding: 5px 10px;
  margin-left: 5px;
}
</style>
