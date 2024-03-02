<script>
import axios from "axios";
export default {
  data() {
    return {
      city: '',
      error: '',
      info: null
    }
  },
  computed: {
    cityName() {
      return "«" + this.city + "»"
    },
    showTemp() {
      return "🌡️ The temperature is: " + Math.round(this.info.data.main.temp) + "°C"
    },
    showFeelsLike() {
      return "🌡️ Feels like: " + Math.round(this.info.data.main.feels_like) + "°C"
    },
    showMinTemp() {
      return "🌡️ Min temperature: " + Math.round(this.info.data.main.temp_min) + "°C"
    },
    showMaxTemp() {
      return "🌡️ Max temperature: " + Math.round(this.info.data.main.temp_max) + "°C"
    },
    showHumidity() {
      return "💧 Humidity: " + this.info.data.main.humidity + "%"
    },
    showPressure() {
      return "🌡️ Pressure: " + this.info.data.main.pressure + "hPa"
    },
    showWind() {
      return "🌬️ Wind speed: " + this.info.data.wind.speed + "m/s"
    },
    showClouds() {
      return "☁️ Clouds: " + this.info.data.clouds.all + "%"
    },
  },
  methods:{
    s() {
      return s
    },
    getWeather(){
      if(this.city.trim().length < 2){
        this.error = "You must enter more than one characters."
        return false
      }
      this.error = ""

      axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&units=metric&appid=3d9de74844d28377e81415151cbe6a66`)
          .then(res => (this.info = res))
    }
  }
}
</script>

<template>
  <div class="wrapper">
    <h1>Weather Forecast App</h1>
    <p>Check the Weather in {{ city == "" ? " your city" :cityName }}</p>
    <input type="text" v-model="city" placeholder="Enter the city">
    <button v-if="city != ''" @click="getWeather()">Get the weather</button>
    <button disabled v-else>Enter your city</button>
    <p class="error">{{ error }}</p>

    <div v-if="info != null" class="info">
      <p>{{ showTemp }}</p>
      <p>{{ showFeelsLike }}</p>
      <p>{{ showMinTemp }}</p>
      <p>{{ showMaxTemp }}</p>
      <p>{{ showHumidity }}</p>
      <p>{{ showPressure }}</p>
      <p>{{ showWind }}</p>
      <p>{{ showClouds }}</p>
    </div>
  </div>
</template>

<style scoped>
.wrapper {
  width: 900px;
  height: 500px;
  border-radius: 50px;
  padding: 20px;
  text-align: center;
  color: #ffffff;
  background-color: rgb(0, 0, 0, 0.8);
  box-shadow: 0 0 10px #fcfcfc;
}

.wrapper h1 {
  margin-top: 50px;
}

.wrapper p {
  margin-top: 20px;
}

.wrapper input {
  margin-top: 30px;
  background: transparent;
  border: 0;
  border-bottom: 2px solid #110813;
  color: #fcfcfc;
  padding: 5px 8px;
  outline: none;
}

.wrapper input:focus {
  border-bottom-color: #5900b0;
}

.wrapper button {
  background: #00ffd9;
  color: #626262;
  font-weight: bold;
  border-radius: 10px;
  border: 0;
  padding: 10px 15px;
  cursor: pointer;
  margin-left: 20px;
  transition: 0.5s ease;
}

.wrapper button:disabled {
  background: #00937b;
  cursor: not-allowed;
}

.wrapper button:hover {
  color: #868686;
  transform: scale(1.05) translateY(-5px);
}

.error{
  color: #ff5050;
}

.info{
  margin-top: 20px;
  display: flex;
  flex-direction: row;
  justify-content: space-around;
  flex-wrap: wrap;
}

.info p {
  margin-top: 20px;
  font-size: 17px;
  font-weight: bold;
  color: #00ffd9;
  background-color: rgba(53, 0, 154, 0.2);
  padding: 15px 10px;
  border-radius: 20px;
  box-shadow: 0 0 10px #00ffd9;
}
</style>