<template>
<div>
  <div v-if="imageUrl" class="weather-widget__location">
    <p>{{locationName}}, {{country}}</p>
    <div class="weather-widget__icon">
      <img :src="imageUrl"/>
      <i>{{temp}} °C</i>
    </div>
    <p>Feels like <b>{{feel}}</b></p>
    <p>{{description}}</p>
  </div>
  <div v-if="!imageUrl && isList" class="weather-widget__location warning">
    <p>{{locationName}}</p>
<p >City not found</p>
  </div>
   <div v-if="!isList" class="weather-widget__location warning">
    <p>{{locationName}}</p>
  </div>
  </div>
</template>

<script lang="ts">
import { Component, Vue, Prop } from 'vue-property-decorator';
import axios from 'axios';

@Component
export default class MainWidget extends Vue {
    @Prop() public locationName!: string;

    imageUrl = '';

    country = '';

    description = '';

    feel = 0;

    temp = 0;

    isList = true;

    mounted() {
      if (this.locationName === 'Add at least one location') {
        this.isList = false;
      } else {
        axios
          .get(`http://api.openweathermap.org/data/2.5/weather?q=${this.locationName}&units=metric&appid=0a1e68fad11848f16008102642b02d79`)
          .then((response: any) => {
            if (response && response.data) {
              this.imageUrl = `http://openweathermap.org/img/wn/${response.data.weather[response.data.weather.length - 1].icon}@2x.png`;
              this.country = response.data.sys.country;
              const descr = response.data.weather[response.data.weather.length - 1].description || '';
              this.description = descr[0].toUpperCase() + descr.substring(1);
              this.feel = Math.round(response.data.main.feels_like);
              this.temp = Math.round(response.data.main.temp);
            }
          });
      }
    }
}
</script>

<style scoped lang="scss">

  .weather-widget__location {
    padding: 10px;
    background-color: #55ffee33;
    margin-bottom: 5px;
    border-radius: 15px;
    box-shadow: 2px 2px 5px gray;
  }
  p {
    margin: 5px;
  }
  .weather-widget__icon {
    justify-content: center;
    display: flex;
    align-items: center;
    font-size: 20px;
    img {
      width: 70px
    }
  }
  .warning {
    color: red;
  }
</style>
