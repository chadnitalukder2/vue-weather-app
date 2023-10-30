<template>
 <div class="app">
  <div class="header container h-100 p-5">
    <h1 class="mb-5">Weather App</h1>
    <div class="d-flex justify-content-center h-100">
      <div class="custom-select ">
  <select style="width: 100%;" class="option" v-model="days">
   
    <option value="2">2 Day</option>
    <option value="4">4 Day</option>
    <option value="6">6 Day</option>
    <option value="8">8 Day</option>
    <option value="10">10 Day</option>
    <option value="15">15 Day</option>
    <option value="20">20 Day</option>
    <option value="25">25 Day </option>
    <option value="30">30 Day</option>
    <option value="35">35 Day</option>
    <option value="40">40 Day</option>
    
  </select>
</div>
      <div class="searchbar w-50 mx-2">
        <input type="text" class="input form-control" v-model="city" placeholder="Enter a city">
      </div>
      <button class="btn-search btn btn-primary" @click="searchWeather">Search	<i class="fa-solid fa-magnifying-glass"></i> </button>
    </div>

  </div>

  <br>

  <weather :city="city" :days="days" v-if="showWeather"></weather>
 </div>
</template>

<script>
import weather from './components/App-Weather.vue'

export default {
  name: 'App',
  components: {
    weather,
  },
  data(){
    return{
      city : '',
      showWeather: false,
      days: '4',
    }
  },
  methods :{
    async searchWeather (){
      if(!this.city){
        alert ("Enter a city name")
        return
      }

      this.showWeather = false;
      await this.$nextTick();
      this.showWeather = true;
    }
  }
}
</script>

<style>
body{
  background: #121212 !important;
}
.header{
  background:#212730 ;
  border-radius: 20px;
  color: #fff;
  text-align: center;
  font-family: 'Franklin Gothic Medium', 'Arial Narrow',sans-serif;
  margin-top: 5rem;
}
.btn-search{
  background-image:linear-gradient(to right, cyan,magenta ) ;
}
.option{
  display: block;
   width: 100%;
    padding: 7px 10px;
    color: #212529;
    font-size: 1rem;
    font-weight: 400;
    line-height: 1.5;
    border-radius: 6px;
    color: var(--bs-body-color);
}
.option:focus{
  background-color: var(--bs-body-bg);
    border-color: #86b7fe;
    outline: 0;
    box-shadow: 0 0 0 0.25rem rgba(13, 110, 253, 0.25);
}

</style>
