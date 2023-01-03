<template class="d">
  <v-container class="mt-6 text-center">

    <v-row>

      <!-- <v-col cols="12" lg="1" class="bg-light">

        <v-icon style="font-size:44px">mdi-apple-icloud</v-icon>
        <br />

        <div class="mt-10">
          <a style="color:black;"><v-icon>mdi-weather-pouring</v-icon>Weather</a>
        </div>

        <div class="mt-8">
          <a style="color:black;"><v-icon>mdi-chart-bar-stacked</v-icon>Cities</a>
        </div>

        <div class="mt-8">
          <a style="color:black;"><v-icon>mdi-map-marker-multiple</v-icon>Map</a>
        </div>

      </v-col> -->

      <v-col cols="12" lg="11">
        <v-text-field label="Search" v-model="searchcity"></v-text-field>
        <v-btn color="primary" elevation="2" @click="searchbycity()">Search</v-btn>
        <div class="weather-data">
          <div>

            <h1 class="city">{{ this.city }}</h1>
            <p class="rain">{{ this.cloud }}</p>
            <p class="condition">{{ this.description }}</p>
            <h3>Temperature</h3>
            <h1 class="temp">
              <v-icon color="#FF0000" class="mr-2" size="40">mdi-thermometer-high</v-icon>{{ this.temp
}}<span>&#176;</span>
            </h1>
          </div>
          <div>
            <img class="img" v-bind:src="this.imgsrc" />
          </div>
        </div>
      </v-col>


    </v-row>

  </v-container>
</template>

<script>
export default {
  name: 'HelloWorld',

  data: () => ({
    // api_key:'b23a35160f22396a2662366f363024be'
    time: "",
    citie: "",
    searchcity: "",
    imgsrc: "",
    rain: '',
    city: "",
    temp: "",
    description: "",
    pressure: "",
    humidity: "",
    visibility: "",
    right: null,
  }),
  methods: {
    searchbycity() {

      console.log(this.searchcity);
      fetch(
        `https://api.openweathermap.org/data/2.5/weather?q=${this.searchcity}&appid=306807ad7cfa2516d41e3318086b059d`
      )
        .then((response) => response.json())
        .then((data) => {
          console.log(data);
          this.time = new Date(data.dt * 1000 + data.timezone * 1000);
          this.city = data.name;
          this.temp = Math.round(data.main.temp_max - 273.15);

          this.description = data.weather[0].description;
          this.pressure = data.main.pressure;
          this.humidity = data.main.humidity;
          this.visibility = data.visibility;
          this.imgsrc = `https://openweathermap.org/img/wn/${data.weather[0].icon}@2x.png`;
        });
    }
  }
}
</script>

<style>
.bg-light {
  background-color: #EAECEF;
}
</style>
