<template> 
  <br>
  <h1><center>Weather</center> </h1>
  <div>
    <div class="widget-border">
        <form @submit.prevent="searchWeather">
          <input type="text" v-model="location" placeholder="Cari Lokasi..."><br>
          <button type="submit">Cek Suhu dan Cuaca</button>
        </form>
        <div v-if="weatherData">
        <h2>{{ weatherData.location }}</h2>
        <p>Suhu : {{ weatherData.temperature }}°C</p>
        <p>Cuaca : {{ weatherData.description }}</p>
        </div>
    </div>
  </div>
</template>


<script scoped>
export default {
data() {
  return {
    location: '',
    weatherData: null,
  };
},
methods: {
  async searchWeather() {
    const apiKey = 'd9cec9d77b0545ac936102418230507'; //API KEY
    const apiUrl = `https://api.weatherapi.com/v1/current.json?key=${apiKey}&q=${this.location}`; //URL API

    try {
      const response = await fetch(apiUrl);
      const data = await response.json();
      this.weatherData = {
        location: data.location.name,
        temperature: data.current.temp_c,
        description: data.current.condition.text,
      };
    } catch (error) {
      console.error('Terjadi kesalahan:', error);
    }
  },
},
};
</script>

<style scoped>
.widget-border {
  width: 700px;
  height: 400px;
  border: 3px solid #333;
  border-radius: 25px;
  padding: 20px;
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  background-color: #f2f2f2;
}

h1{
  font-size: 40px;
  color: #333;
}

input {
  width: 300px;
  vertical-align: middle;
  white-space: nowrap;
  position: relative;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
  outline: none;
  transition: border-color 0.3s ease;
  margin-top: -220px;
  font-size: medium;
}

input:focus {
  border: 2px solid #333;
}

button {
  margin-top: 50px;
  display: block;
  margin: 0 auto; 
  background-color: #ff0000;
  color: #ffffff; 
  font-size: 18px; 
  padding: 10px 20px; 
  border-radius: 5px;
  margin-top: -80px;
}

button:hover{
  background: #db0000;
  color: #d1cfcf;
  text-decoration: none;
}

</style>