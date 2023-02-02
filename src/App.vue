<template>
  <div class="flex flex-col justify-center items-center h-[100vh]">
    <div class="bg-gray-200 pb-10 pt-2 border rounded-[10px]">
      <Header @name-city="searchCity"/>
      <div class="flex justify-center">
          <div class="bg-blue-100 bg-image p-4 border rounded-[10px]">
              <div class="flex items-center justify-start">
                  <div class="flex bg-white-300 mr-4">
                      <img src="./assets/icons/sun.png" alt="icon" class="w-8">
                  </div>
                  <div>
                      <p class="text-lg font-semibold ">Weather in {{ data?.name }}</p>
                      <p>{{ desc }}</p>
                  </div>
              </div>
              <div class="flex items-center">
                <h1 class="font-bold text-6xl mr-4">{{ Math.round(data?.main?.feels_like ) }}°C</h1>
                <h4 class="ml-4 px-2 border rounded-[6px]" style="background-color: white">{{ Math.round(data?.main?.temp_min) }}°C</h4>
              </div>
              <div class="flex justify-start items-center">
                  <img :src="`http://openweathermap.org/img/wn/${ icon }@2x.png`" alt="icon" class="icon" />
                  <div class="description">{{ weather }}</div>
              </div>
              <div><b>Humidity: </b>{{ data?.main?.humidity }}%</div>
              <div><b>Wind speed: </b>{{ data?.wind?.speed }}km/h</div>
          </div>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from '@vue/reactivity'
import axios from 'axios'
import Header from './components/Header.vue';
import Weather from './components/Weather.vue';

export default {
  components: {
    Header,
    Weather
  },
  setup() {
    const data = ref('')
    const desc = ref('')
    const weather = ref('')
    const icon = ref('')
    const searchCity = async (argument) => {
        try {
            const res = await axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${argument || 'Ha Noi'}&appid=d41de7b99a0b585bef96b7a4886b27dc&units=metric&lang=vi`)
            data.value = res.data
            desc.value = res.data?.weather[0]?.description
            weather.value = res?.data.weather[0]?.main
            icon.value = res?.data?.weather[0]?.icon
            console.log(res.data)
        } catch (error) {
            console.log(error)
        }
    }
    searchCity()
    return {
      data,
      desc,
      weather,
      icon,
      searchCity
    }
  },
}
</script>


<style scoped>
    .bg-image {
        background: url('./assets/icons/sunset.png');
        background-repeat: no-repeat;
    }
</style>