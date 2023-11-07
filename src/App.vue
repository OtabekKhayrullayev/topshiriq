<script>
import axios from "axios";
export default {
  data() {
    return {
      city: "",
      country: "",
      temp: "",
      con: "",
      word: "",
    };
  },
  methods: {
    async submit() {
      const response = await axios.get(
        `https://api.openweathermap.org/data/2.5/weather?q=${this.word}&units=metric&APPID=38c126d5e32eab21fd35a4d2f1fb0881`
      );
      // console.log(response.data);
      this.city = response.data.name;
      this.country = response.data.sys.country;
      this.con = response.data.weather[0].main;
      this.temp = response.data.main.temp;
    },
  },
};
</script>

<template>
  <section :class="{ cold: temp < 16, hot: temp >= 16 }">
    <div class="container">
      <div class="text">
        <form @submit.prevent="submit" style="margin-top: 15px">
          <input
            type="text"
            placeholder="enter the name of the city"
            v-model="word"
            style="background-color: #fff7; outline: none; border: none"
          />
        </form>
      </div>
      <div class="test">
        <div class="test__city">
          <span>{{ city }} </span>
          <span v-if="city">,</span>
          <span> {{ country }}</span>
        </div>
        <div class="test__date">
          <span>{{ String(new Date()).slice(0, 15) }}</span>
        </div>
        <template v-if="temp">
          <div class="test__c">
            <div class="test__t">
              <span>{{ temp.toFixed(0)}}&deg;C</span>
            </div>
          </div>
        </template>
        <div class="test__weather">
          <h3>{{ con }}</h3>
        </div>
      </div>
    </div>
  </section>
</template>

<style>
html {
  font-size: 25px;
}
.container {
  max-width: 1200px;
  margin-right: auto;
  margin-left: auto;
}
.test {
  text-align: center;
  /* margin-top: 50px; */
}
.test * {
  color: #000;
}
.text {
  display: flex;
  justify-content: center;
}
.text input {
  padding-top: 8px;
  padding-bottom: 8px;
  /* padding-right: 80px; */
  box-shadow: 0 0 5px 3px #0000001c;
  border: none;
  border: 1px solid #000;
  border-top-right-radius: 10px;
  border-bottom-left-radius: 10px;
  background-color: #03c8f9;
  /* opacity: .2; */
  padding-left: 5px;
  margin-bottom: 50px;
  font-size: 25px;
}
.cold {
  height: 90vh;
  /* background-size: cover; */
  background-repeat: no-repeat;
  background-image: url(https://raw.githubusercontent.com/TylerPottsDev/weather-vue/master/src/assets/cold-bg.jpg);
  background-position: center;
  transition: all 0.5s ease-in-out;
}
.hot {
  height: 90vh;
  /* background-size: cover; */
  background-repeat: no-repeat;
  background-image: url(https://raw.githubusercontent.com/TylerPottsDev/weather-vue/master/src/assets/warm-bg.jpg);
  background-position: center;
  transition: all 0.5s ease-in-out;
}
.test__city {
  margin-bottom: 5px;
}
.test__city span {
  font-size: 30px;
}
.test__date {
  margin-bottom: 20px;
  font-style: italic;
}
.test__c {
  padding: 50px 20px;
  font-size: 50px;
  max-width: max-content;
  margin-right: auto;
  margin-left: auto;
  background-color: #fff5;
  border-radius: 10px;
  /* opacity: 0.1; */
  font-weight: bold;
  font-family: sans-serif;
  position: relative;
}

.test__t span {
  /* position: absolute;
  left: 46%;
  top: 25%; */
  color: #000;
  font-size: 60px;
  font-weight: bold;
  color: #fff;
  text-shadow: -1px 3px 2px rgba(0, 0, 0, 0.39);
}
.test__weather {
  font-style: italic;
  font-weight: bold;
  font-size: 50px;
}
</style>
