<template>
  <div class="app">
    <div class="container p-0">

      <div class="d-flex">
        <div class="card main-div w-100">
          <div class="p-3">
            <h2 class="mb-1 day">Today</h2>
            <p class="text-light date mb-0">{{ date }}</p>
            <small>{{ time }}</small>
            <h2 class="place">
              <i class="fa fa-location">{{ name }} <small>{{ country }} </small></i>
            </h2>
            <div class="temp">
              <h1 class="weather-tem">{{ temperature }}&deg;</h1>
              <h2 class="text-light">{{ description }} <img :src="iconUrl"></h2>
            </div>
          </div>
        </div>

        <div class="card card-2 w-100">
        <table class="m-4">
          <tbody>
            <tr>
              <th>Sea Level</th>
              <td v-if="sea_level > 0">{{ sea_level }}</td>
              <td v-else>Null</td>
            </tr>
            <tr>
              <th>Humidity</th>
              <td>{{ humidity }}</td>
            </tr>
            <tr>
              <th>Wind</th>
              <td>{{ wind }}</td>
            </tr>
          </tbody>
        </table>
        <DaysWaeather :cityname="cityname"></DaysWaeather>
        <div id="div_form" class="d-flex m-3 justify-content-center">
          <form>
            <input
            @click="changeLocation()"
              type="button"
              value="Change Location"
              class="btn change_btn change-btn btn-primary"
            />
          </form>
        </div>
      </div>
    
      </div>

     
    </div>
  </div>
</template>
<script>
import axios from 'axios';
import DaysWaeather from './App-daysWeather.vue'
export default {
  name: "myWeather",
  components : {
    DaysWaeather,
  },
  props:{
    city: String,
  },
  data(){
    return{
      cityname: this.city,
      temperature:null,
      description: null,
      iconUrl: null,
      date: null,
      time: null,
      name: null,
      sea_level: null,
      humidity: null,
      wind: null,
      country: null,
      monthName: ["January", "February", "March", "April", "May", "June", "July", "August", "september", "October", "November", "December"],
    }
  },
  methods:{
    changeLocation(){
      window.location.reload();
    }
  },
  async created(){
    const response = await axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&units=metric&appid=8331cdef4f10633c84fd856ce65588b0`)
    const weatherDate = response.data;
    this.temperature = Math.round (weatherDate.main.temp);
    this.description = weatherDate.weather[0].description;
    this.name = weatherDate.name;
    this.wind = weatherDate.wind.speed;
    this.sea_level = weatherDate.main.sea_level;
    this.country = weatherDate.sys.country;
    this.humidity = weatherDate.main.humidity;

    this.iconUrl = `https://api.openweathermap.org/img/w/${weatherDate.weather[0].icon}.png`;
    const d = new Date();
    this.date = d.getDate() + ':' + this.monthName[d.getMonth()] + ':' + d.getFullYear();
    this.time = d.getHours() + ':' + d.getMinutes() + ':' + d.getSeconds();

    console.log(weatherDate);
  }
};
</script>
<style scoped>
body {
  background-color: #343d4d;
}
.weather-temp {
  margin: 0;
  font-weight: 700;
  font-size: 4em;
}
h2.mb-1.day {
  font-size: 3rem;
  font-weight: 400;
}
.main-div {
  border-radius: 20px;
  color: #fff;
  background-image: url(https://t3.ftcdn.net/jpg/05/56/54/54/360_F_556545409_Uf0E75VSj0L48wLKgascatY5pzKblQzQ.jpg);
  background-size: cover;
  background-position: center;
  background-color: rgba(0, 0, 0, 0.5);
  background-repeat: no-repeat;
}
.temp {
  position: absolute;
  bottom: 0;
}
.main-div:hover {
  transform: scale(1.1);
  transition: transform 0.5s ease;
  z-index: 1;
}
.card-2 {
  background-color: #212730;
  border-radius: 20px;
}

.card-details {
  margin-left: 19px;
}
.h1_left{
    position: absolute;
    bottom: 25px;
    left: 16px;
    font-size: 3vw ;
    line-height: 1.2;
}
.h3_left{
    position: absolute;
    left: 16px;
    font-size: 2vw ;
    line-height: 0.5;
}
.h3_left small{
    font-size: 1rem;
}
table{
    position: relative;
    left: 15px;
    border-collapse: separate;
    border-spacing: 15px ;
    text-align: left;
    max-width: 600px;
    margin: 0 auto;
}
th,td{
    font-size: 18px;
    color: #fff;
}
td{
    text-align: right;
}
table, tr:hover{
    color: red;
}
.change_btn{
    background-image:linear-gradient(to right, cyan, magenta) ;
}
.change_btn:hover{
    transform: scale(0.9);
    transition: transform 0.1s ease;
}
</style>
