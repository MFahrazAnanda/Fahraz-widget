<template>
  <div class="location-widget">
    <h2>Location</h2>
    <div v-if="latitude && longitude">
      <p>Garis Lintang : {{ latitude }}</p>
      <p>Garis Bujur : {{ longitude }}</p>
    </div>
    <div v-else>
      <p>Mencari Locari Kamu...</p>
    </div>
    <div class="location-input">
      <label for="latitude">Garis Lintang</label>
      <input type="text" id="latitude" v-model="inputLatitude" />
    </div>
    <div class="location-input">
      <label for="longitude">Garis Bujur</label>
      <input type="text" id="longitude" v-model="inputLongitude" />
    </div>
    <button @click="fetchLocationDetails" class="tombol">Menemukan Detail Lokasi</button>
    <div v-if="foundLocation" class="out">
      <h3>Lokasi Detail</h3>
      <p>{{ foundLocation.components.country }}</p>
      <p>{{ foundLocation.components.city }}</p>
      <p>{{ foundLocation.components.street }}</p>
      <p>Postal Code: {{ foundLocation.components.postcode }}</p>
    </div>
  </div>
</template>
  
<script>
  export default {
    data() {
      return {
        latitude: null,
        longitude: null,
        inputLatitude: '',
        inputLongitude: '',
        foundLocation: null,
      };
    },
    mounted() {
      if (navigator.geolocation) {
        navigator.geolocation.getCurrentPosition(this.getPosition);
      }
    },
    methods: {
      getPosition(position) {
        this.latitude = position.coords.latitude;
        this.longitude = position.coords.longitude;
      },
      async fetchLocationDetails() {
        try {
          const apiKey = '92591005a7b94008909d59a64b6d2a49';
          const latitude = this.inputLatitude || this.latitude;
          const longitude = this.inputLongitude || this.longitude;
          const apiUrl = `https://api.opencagedata.com/geocode/v1/json?q=${encodeURIComponent(
            latitude + ',' + longitude
          )}&key=${apiKey}`;
  
          const response = await fetch(apiUrl);
          const data = await response.json();
  
          if (data.results && data.results.length > 0) {
            const location = data.results[0];
            this.foundLocation = location;
            console.log('Location:', location);
          }
        } catch (error) {
          console.error('Error fetching location data:', error);
        }
      },
    },
  };
</script>
  
<style scoped>
.location-widget {
  width: 700px;
  height: 630px;
  margin: 0 auto;
  font-size: 20px;
  border: 3px solid #333;
  border-radius: 25px;
  padding: 20px;
  margin-bottom: 20px;
  text-align: center;
  background-color: #f2f2f2;
  }
  
.location-widget h2 {
  color: #333;
  font-size: 34px;
  margin-bottom: 50px;
  margin-top: 15px;
}
  
.location-widget p {
  color: #333;
}
  
.location-input {
  margin-top: 50px;
}
  
.location-input label {
  display: block;
  margin-bottom: 5px;
  color: #333;
  font-size: 18px;
  font-style: bold;
}
  
.location-input input {
  width: 200px;
  padding: 10px;
  margin-right: 10px;
  border: 2px solid #333;
  border-radius: 5px;
  font-size: 18px;
  font-style: bold;
}
  
.tombol {
  display: block;
  margin: 0 auto; 
  background-color: #ff0000;
  color: #ffffff; 
  font-size: 18px; 
  padding: 10px 20px; 
  border-radius: 5px;
  margin-top: 30px;
}
  
.tombol:hover {
  background: #db0000;
  color: #d1cfcf;
  text-decoration: none;
}
  
.tombol:disabled {
  background-color: #ccc;
  color: #999;
  cursor: not-allowed;
}
  
.out {
  margin-top: 20px;
}
  
.out h3 {
  margin-bottom: 20px;
  color: #333;
  font-size: 18px;
}
  
.out p {
  margin: 15px 0;
  color: #333;
}
</style>
  