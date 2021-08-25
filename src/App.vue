<template>
  <div id="app">
    <main>
      <input type="text"
      placeholder="escribe una ciudad"
      v-model="query" 
      @keypress="fetchWeather"/>
    </main>
    <div v-if="typeof weather.main != 'undefined'">
      <br>
      {{weather.name}}, {{weather.sys.country}}
      <br>
      <h1>{{ Math.round(weather.main.temp) }}º</h1>
      <h6>{{weather.weather[0].main}}</h6>
      <br>
      <p>I ❤️ Cibi</p>
    </div>
  </div>
</template>

<script>

export default {
  name: 'App',
  data () {
    return {
      api_key: '852e042da4d812d7f4d459a315c36d72',
      url_base: 'https://api.openweathermap.org/data/2.5/',
      query: '',
      weather: '',
    }
  },
  methods: {
    fetchWeather (e) {
      if (e.key == "Enter") {
        fetch(`${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`)
          .then( res => {
            return res.json();
          }).then(this.setResults)
      }
    },
    setResults (results) {
      this.weather = results;
    }
  }
}
</script>

<style>

  body {
    background: lightgrey;
  }

  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }

  input {
    padding: 10px;
    font-size: 20px;
  }

</style>
