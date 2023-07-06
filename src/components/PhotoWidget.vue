<template>
  <div class="photo-widget">
      <h1 class="ket1">Widget Photo</h1>
    <div class="image-container">
      <img :src="currentPhoto" :alt="currentPhoto" :style="{ width: '1000px', height: 'auto' }" />
    </div>
    <div class="controls-foto">
      <button @click="prevPhoto">Kembali</button>
      <button @click="nextPhoto">Selanjutnya</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      photos: [require('../assets/photo1.jpg'),
      require('../assets/photo2.jpg'),
      require('../assets/photo3.jpg'),
      require('../assets/photo4.jpg'),
      require('../assets/photo5.jpg'),
      require('../assets/photo6.jpg'),
      require('../assets/photo7.jpg'),
      require('../assets/photo8.jpg'),
      require('../assets/photo9.jpg'),
      require('../assets/photo10.jpg')],
      currentIndex: 0,
    };
  },
  computed: {
    currentPhoto() {
      return this.photos[this.currentIndex];
    },
  },
  methods: {
    kembaliKeBeranda() {
      this.$router.push('/beranda')
    },
    prevPhoto() {
      if (this.currentIndex > 0) {
        this.currentIndex--;
      } else {
        this.currentIndex = this.photos.length - 1;
      }
    },
    nextPhoto() {
      if (this.currentIndex < this.photos.length - 1) {
        this.currentIndex++;
      } else {
        this.currentIndex = 0;
      }
    },
  },
};
</script>

<style scoped>
.ket1 {
  font-weight: bold;
  margin-bottom: 50px;
  margin-top: -50px;
  color: #333;
  font-family: 'Open Sans',sans-serif;
}

.photo-widget {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 90vh;
}

.image-container {
  margin-bottom: 20px;
  border: 30px solid #333; 
  border-radius: 25px;
  padding: 5px;
  display: flex;
  justify-content: center;
}
.image-container img {
  max-width: 100%;
  max-height: 100%;
}

.controls-foto button {
  padding: 15px 25px;
  font-size: 18px;
  background-color: #ff0000;
  color: #fff;
  border: none;
  cursor: pointer;
  transition: background-color 0.3s ease;
  border-radius: 20px;
  margin-right: 10px;
  font-weight: bold;
}

.controls-foto button:hover {
  background: rgb(255, 112, 112);
  color: #d1cfcf;
  text-decoration: none;
}

</style>