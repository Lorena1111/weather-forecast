<template>
  <main class="main" :style="'background:' + appBackground">
    <!-- v-if="weatherData" znači ako postoje podaci u weatherdata, odnosno kad postoje, tada se krene izvršavat sve dalje: -->
    <div class="weather-box" v-if="weatherData">
      <p>Odaberite lokaciju:</p>
      <!-- lokaciju koju upišemo spremimo u city u datu pomoću v-modela.
      na enter pokreni funkciju getweatherinfo: -->
      <input
        type="text"
        v-model="city"
        placeholder="Upiši lokaciju"
        v-on:keyup.enter="getWeatherInfo"
      />
      <!-- i na klik buttona pokreni getWeatherInfo -->
  
      <button type="button" @click="getWeatherInfo">Pretraži</button> <br>
      ili
      <button type="button" @click="getCurrentLocation" style="margin-top: 4px">
        Dohvati lokaciju
      </button>
      <!-- ako postoji poruka, ispiši, ako ne ne: -->
      <p v-if="errorMessage">{{ errorMessage }}</p>
      <h2>Vrijeme u: {{ weatherData.name }}</h2>
      <!-- zaokružimo na 0 decimala sa toFixed(0): -->
      <p>Temperatura: {{ weatherData.main.temp.toFixed(0) }}°C</p>
      <div class="weather-icon-desc">
        <img
          :src="
            'http://openweathermap.org/img/wn/' +
            weatherData.weather[0].icon +
            '.png'
          "
        />
        <p>
          {{ weatherData.weather[0].description }}
        </p>
      </div>

      <p>Vlažnost: {{ weatherData.main.humidity }}%</p>
      <p>Brzina vjetra: {{ weatherData.wind.speed }} m/s</p>
    </div>
  </main>
</template>

<script>
export default {
  data() {
    return {
      weatherData: undefined,
      city: 'Rijeka',
      errorMessage: '',
    }
  },
  created() {
    //na pokretanje stranice zovemo:
    this.getWeatherInfo()
  },
  methods: {
    // metoda koja dohvaća i sprema podatke s apija u this.weatherdata:
    getWeatherInfo() {
      this.errorMessage = '' // pri pokretanju funkcije poništimo prijašnje poruke za greške
      this.$axios
        .get(
          `https://api.openweathermap.org/data/2.5/weather?q=${this.city}&units=metric&appid=dfa0a1b105a9fe2d20fc4cdcd01c04af`
        )
        .then((res) => {
          this.weatherData = res.data
        })
        .catch((error) => (this.errorMessage = 'Lokacija nije pronađena.'))
    },
    getCurrentLocation() {
      this.errorMessage = ''
      if (navigator.geolocation) {
        navigator.geolocation.getCurrentPosition(this.onSuccess, this.onError)
      }
    },
    onSuccess(position) {
      const { latitude, longitude } = position.coords
      this.$axios
        .get(
          `https://api.openweathermap.org/data/2.5/weather?lat=${latitude}&lon=${longitude}&units=metric&appid=dfa0a1b105a9fe2d20fc4cdcd01c04af`
        )
        .then((res) => {
          this.weatherData = res.data
          this.city = res.data.name
        })
    },
    onError(error) {
      this.errorMessage = error.message
    },
  },
  computed: {
    appBackground() {
      if (
        this.weatherData &&
        this.weatherData.weather[0].description.includes('rain')
      )
        // ako postoje podaci i ako descrition sadrži riječ 'rain', vrati sljedeću boju
        return 'linear-gradient(45deg, #6f9ba1, #2c2c2c)'
      if (
        this.weatherData &&
        this.weatherData.weather[0].description.includes('clear')
      )
        return 'linear-gradient(45deg, #aef5ff, #ffe000)'
      if (
        this.weatherData &&
        this.weatherData.weather[0].description.includes('clouds')
      )
        return 'linear-gradient(45deg, #aef5ff, #444)'
    },
  },
}
</script>

<style >
body {
  margin: 0;
  padding: 0;
}
input {
  padding: 8px;
  border-radius: 4px;
  border-style:groove;
}


button {
  padding: 6px;
  
}

button:hover{
    font-style: bold;
    font-size:20px;
    filter: drop-shadow(0px 10px 3px black);
    color:white;
}
.main {
  height: 100vh;
  width: 100vw;
  background-color: aliceblue;
  display: flex;
  align-items: center;
  justify-content: center;
  font-family: Arial, Helvetica, sans-serif;
}
.weather-box {
  background: linear-gradient(45deg, #7780a8, #0950c3ce);
  padding: 20px;
  border-radius: 10px;
  filter: drop-shadow(0px 15px 5px black);
  color: white;
  width: 350px;
}
.weather-icon-desc {
  display: flex;
}
</style>