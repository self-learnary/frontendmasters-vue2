<template>
    <div class="location-contain">
      <div class="locations">
        <div class="place">
          <img :src="imgSrc" width="235" height="300"/>
          <h2>{{ cityName }}</h2>
          <p>{{ description }}</p>
        </div>
      </div>
    </div>
</template>
<script>
export default {
    props: ['imgSrc', 'cityName', 'description'],
}
</script>
<style scoped>
.location-contain {
  display: flex;
  justify-content: center;
}

.place {
  display: flex;
  flex-direction: column;
  width: 280px;
  height: 320px;
  justify-content: center;
  background: white;
  border: 1px solid #ddd;
  padding: 20px 20px;
  margin: 10px;
}

.place h2 {
  margin: 0;
  text-align: center;
}

.place img {
  margin: 10px;
  align-self: center;
}
</style>