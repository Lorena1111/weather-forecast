<template>
  <main class="main">
    <div class="weather-boxTwo" v-if="weatherData">
      <div>
        <p>Upišite lokaciju:</p>
        <!-- pritiskom entera se pokrene pretraživanje -->
        <input
          type="text"
          v-model="city"
          placeholder="Odaberi lokaciju"
          v-on:keyup.enter="getWeatherInfo"
        />
        <!-- i klikom na button se isto pokrene pretraživanje -->
        <button type="button" @click="getWeatherInfo">Pretraži</button>
        ili
        <button type="button" @click="getCurrentLocation">Moja lokacija</button>
        <p v-if="errorMessage">{{ errorMessage }}</p>
        <h2>Petodnevna prognoza za {{ weatherData.city.name }}:</h2>
      </div>
      <div class="weather-5day" v-if="middays.length">
        <!-- sa :class dinamički dodijelimo klasu selected onoj koja je kliknuta, tj čini dt_txt sadrži izabrani datum -->
        <div
          v-for="(item, i) in middays"
          :key="i"
          class="weather-1day"
          :class="{ selected: item.dt_txt.slice(0, 10) == chosenDate }"
          @click="selectDay(item)"
        >
          <!-- iz dt podatka izvlačimo dan u tjednu i datum. pošaljemo dt u 2 funkcije: -->
          <p>{{ theWeekday(item.dt) }}, {{ theDate(item.dt) }}</p>

          <p>{{ item.main.temp.toFixed(0) }}°C</p>
          <div class="weather-icon-desc">
            <img
              :src="
                'http://openweathermap.org/img/wn/' +
                item.weather[0].icon +
                '.png'
              "
            />
          </div>
        </div>
      </div>

      <div v-if="hourlyWeather.length">
        <p class="hourly-title"></p>

        <div class="weather-hourly">
          <div
            v-for="(item, i) in hourlyWeather"
            :key="i"
            class="weather-1hour"
          >
            <!-- slice(11, 16): izreži od 11. mjesta do 16. i prikaži: -->
            <p>{{ item.dt_txt.slice(11, 16) }} h</p>
            <p>{{ item.main.temp.toFixed(0) }}°C</p>
            <div class="weather-icon-desc">
              <img
                :src="
                  'http://openweathermap.org/img/wn/' +
                  item.weather[0].icon +
                  '.png'
                "
              />
            </div>
            <div>
              <p>Vlažnost: {{ item.main.humidity }}%</p>
              <p>Vjetar: {{ item.wind.speed }} m/s</p>
            </div>
          </div>
        </div>
      </div>
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
      middays: [],
      hourlyWeather: [],
      chosenDate: '',
    }
  },
  created() {
    // pri pokretanju stranice pozivamo api za podatke
    this.getWeatherInfo()
    // pri pokretanju stranice čekamo 300ms pa pozovemo selectday funkciju. čekamo jer nam prvo trebaju podaci iz getweatherinfo funkcije
    setTimeout(() => {
      this.selectDay()
    }, 300)
  },
  methods: {
    getWeatherInfo() {
      this.errorMessage = ''
      this.$axios
        .get(
          `https://api.openweathermap.org/data/2.5/forecast?q=${this.city}&units=metric&appid=dfa0a1b105a9fe2d20fc4cdcd01c04af`
        )
        .then((res) => {
          this.weatherData = res.data
          // odmah kad dobijemo sve podatke s apija pokrenemo funkciju za određivanje 5 dana i njihovih informacija:
          this.listOfMiddays()
        })
        .catch((error) => (this.errorMessage = 'Location not found.'))
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
          `https://api.openweathermap.org/data/2.5/forecast?lat=${latitude}&lon=${longitude}&units=metric&appid=dfa0a1b105a9fe2d20fc4cdcd01c04af`
        )
        .then((res) => {
          this.weatherData = res.data
          this.city = res.data.name
        })
    },
    onError(error) {
      this.errorMessage = error.message
    },
    // idi kroz weatherdata i nađi podatke koji sadrže 12: u dt_txt. 12 jer je sredina dana, pa prikažemo podatke za to vrijeme:
    listOfMiddays() {
      const res = this.weatherData.list.filter((item) =>
        item.dt_txt.includes('12:')
      )
      this.middays = res
    },

    // na klik jednog dana pokreni ovu funkciju:
    selectDay(item) {
      // varijabla day je na početku nepoznata. ako postoji item, day je item. ako ne postoji item, day je prvi u listi midday-a:
      let day = undefined
      if (item) {
        day = item
      } else {
        day = this.middays[0]
      }
      if(day){
      // izreži prvih 10:
      const date = day.dt_txt.slice(0, 10)
      // idi kroz listu i nađi sve koji sadžre ovaj gore datum (date). to je datum od kliknutog elementa.sprema se u hourlyweater
      this.hourlyWeather = this.weatherData.list.filter((element) =>
        element.dt_txt.includes(date)
      )
      // spremimo datum u chosendate, trebat će nam zbog klase gore
      this.chosenDate = date
    } 
    },

    // iz dt-a pronađemo dan u tjednu
    theWeekday(timestamp) {
      const days = ['Ned', 'Pon', 'Uto', 'Sri', 'Čet', 'Pet', 'Sub']
      const weekday = new Date(timestamp * 1000).getDay()
      return days[weekday]
    },
    theDate(date) {
      const d = new Date(date * 1000)
      const day = d.getDate()
      const month = d.getMonth() + 1
      const year = d.getFullYear()
      return `${day}.${month}.${year}`
    },
  },
}
</script>

<style>
body {
  margin: 0;
  padding: 0;
  font-family: Calibri, 'san-serif';
}
p {
  margin: 4px 0;
}
input {
  padding: 8px;
  border: none;
  border-radius: 4px;
  color:White;
}
button {
  padding: 6px;
}
.main {
  height: 100vh;
  width: 100vw;
  background-image: url('https://images.unsplash.com/photo-1592210454359-9043f067919b?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxzZWFyY2h8NHx8d2VhdGhlcnxlbnwwfHwwfHw%3D&auto=format&fit=crop&w=500&q=60');
  background-repeat:repeat;
    background-size: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
}
.weather-boxTwo {
  background: linear-gradient(45deg, #7780a8, #0950c3ce);
  padding: 20px;
  border-radius: 10px;
  color: white;
  filter: drop-shadow(5px 15px 5px black);
}
.weather-icon-desc {
  display: flex;
}

.weather-5day {
  /* display: flex; */
  display: grid;
  grid-template-columns: repeat(5, 1fr);
}
.weather-1day {
  margin-right: 10px;
  border: 1px solid white;
  padding: 0 5px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  cursor: pointer;
}
.selected {
  border-color: #daa404;
}

.weather-hourly {
  display: grid;
  grid-template-columns: repeat(8, 1fr);
  gap: 10px;
}

.hourly-title {
  margin-top: 20px;
  margin-bottom: 10px;
}

.weather-1hour {
  padding: 0 5px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}
</style>