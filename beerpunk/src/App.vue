<template>
  <div id="app">
    <h1>Make yourself your punk beer!</h1>
    <div v-if="beers.length === 0" class="loading">Loading...</div>
    <div :key="beer.id" v-for="beer in beers" class="beer-contain">
      <div class="beer-img">
        <img :src="beer.img" style="height: 350px;" alt="">
      </div>
      <div class="beer-info">
        <h2>{{ beer.name }}</h2>
        <p class="bright">{{ beer.tagline }}</p>
        <p><span class="bright">Description:</span> {{ beer.desc }}</p>
        <p><span class="bright">Tips:</span> {{ beer.tips }}</p>
        <h3 class="bright">Food pairings</h3>
        <ul>
          <li v-bind:key="`item-${index}`" v-for="(item, index) in beer.food" >
            {{ item }}
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'App',
  components: {
  },
  data(){
    return {
      bottom: false,
      beers: [],
    }
  },
  watch: {
    bottom(bottom){
      if(bottom){
        this.addBeer()
      }
    }
  },
  created(){
    window.addEventListener('scroll', () => {
      this.bottom = this.bottomVisible()
    })
    this.addBeer()
  },
  methods: {
    bottomVisible(){
      const scrollY = window.scrollY
      const visible = document.documentElement.clientHeight
      const pageHeight = document.documentElement.scrollHeight
      const bottomOfPage = visible + scrollY >= pageHeight
      return bottomOfPage || pageHeight < visible
    },
    addBeer(){
      this.axios.get('https://api.punkapi.com/v2/beers/random')
       .then(response => {
         let api = response.data[0];
         let apiInfo = {
           id: api.id,
           name: api.name,
           desc: api.desc,
           img: api.image_url,
           tips: api.brewers_tips,
           tagline: api.tagline,
           food: api.food_pairing
         };
         this.beers.push(apiInfo)
         if(this.bottomVisible()){
           this.addBeer
         }
       })
    }
  }
}
</script>
<style scoped>
body {
  font-family: 'Archivo Narrow', sans-serif;
  background: #25859a;
}

h1, h2, h3, h4 {
  font-family: 'Fjalla One', sans-serif;
}

h1 {
  margin-top: 40px;
  color: white;
  text-align: center;
}

.loading {
  color: white;
  text-align: center;
  font-size: 20px;
}

.display {
  display: flex;
  justify-content: center;
  align-content: center;
}

#app {
  flex-direction: column;
}

.beer-contain {
  width: 50%;
  margin: 20px 24%;
  box-shadow: 0 2px 3px 1px rgba(30, 0, 0, 0.1);
}

.beer-img {
  padding: 30px;
  background: #FF6542;
  border: 1px solid #88498F;
  border-right: 1px solid #f44822;
}

.beer-info {
  background: #564154;
  color: white;
  padding: 30px;
  border: 1px solid #88498F;
}
.beer-info .bright {
    color: #fcd7cf;
    font-family: 'Contrail One', sans-serif;
  }

h3 {
  margin-bottom: 5px;
}

ul {
  margin-top: 5px;
}
</style>