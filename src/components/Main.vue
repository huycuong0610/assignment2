<template>
  <div>
    <div class="grid">
       <div class="title leftTop">
        {{ tiles.datetime.content.date  }} <br/>
        {{ tiles.datetime.content.time  }}
      </div>
      <div class="title center">
        <img src="@/assets/img/weather.svg" />
      </div>
      <div class="title rightTop">
          {{ tiles.temperature.content }}
      </div>
     <div class="title leftBottom">
          {{ tiles.location.content }}
      </div>
       <div class="title rightBottom">
          {{ tiles.description.content }}
      </div>
      <Nav :data="tiles.nav" :changeLocation="this.changeLocation"/>
    </div>
  </div>
</template>

<script>
import Nav from '@/components/Nav'

export default {
  name: 'Main',
  components: { Nav },
  data () {
    return {
      greetingmsg: 'Welcome to Weatherly!',
      currentCity: 'Stockholm',
      tiles: {
        datetime: {
          title: 'leftTop',
          content: {
            date: new Date().toLocaleDateString(),
            time: new Date().toLocaleTimeString()
          }
        },
        weather: {
          content: 'Current Weather'
        },
        temperature: {
          content: '24 deg'
        },
        location: {
          content: ''
        },
        description: {
          content: 'Sunny with clear skies'
        },
        nav: {
          content:
          [
            'Stockholm',
            'Hanoi',
            'Paris',
            'London',
            'Beijing'
          ]
        }
      },
      apiData: {}
    }
  },
  methods: {
    fetchData () {
      let self = this
      let api = `https://api.openweathermap.org/data/2.5/find?q=${this.currentCity}&units=metric&appid=dfe15a41201d660911d013203832e676`
      fetch(api).then(function (response) {
        return response.json()
      }).then(function (result) {
        self.apiData = result
        self.tiles.location.content = result.list[0].name
        self.tiles.temperature.content = Math.floor(result.list[0].main.temp)
        self.tiles.description.content = result.list[0].weather[0].description
        self.tiles.datetime.content.date = Date(result.list[0].dt).toLocaleDateString()
      })
    },
    changeLocation (city) {
      let self = this
      self.currentCity = city
      this.fetchData()
    }
  },
  mounted () {
    this.fetchData()
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
