<script >
import modeImg from "./assets/images/mode.svg";

export default {

  data() {
    return {
      name: "sardor",
      countrys: [],
      theme: false,
      load: true,
      imgMode: modeImg,
    }
  }, 

  methods: {
// fetch api
    async getCountry(){
      try {
        const res = await fetch('https://restcountries.com/v2/all');
        const data = await res.json();
        this.countrys = data;
        this.load = false;
        console.log(data);
      }catch (error) {
        console.log(error);
      }
    },
//      < end! />
// dark mode cheats
    darkMode(){
      const body = document.querySelector('body')
      this.theme = !this.theme;
      const bg = this.theme ? 'dark' : 'light';
       window.localStorage.setItem('theme',bg);
      this.changeMode();
    },

    changeMode(){
      if(window.localStorage.getItem('theme') == 'dark'){
      document.querySelector('body').classList.add('dark');
    }else{
      document.querySelector('body').classList.remove('dark');
    }
    }
//      < end! />
  },
  

  mounted(){
    this.getCountry();
    this.changeMode();
  },

};

</script>

<template>
    <header>
    <div class="container">
      <div class="wrap">
        <h1 class="title">Countries</h1>
        <div class="box">
          <form>
            <input type="search" class="search js-input" placeholder="search">
          </form>
          <select class="select js-select">
            <option value="Filter region" disabled="" selected="">Filter region</option>
          </select>
          <button @click="darkMode" class="mode js-mode">
            <img class="mode-img" :src="imgMode" alt="">
          </button>
        </div>
      </div>
    </div>
  </header>

  <div class="container">
    <div v-if="load"  class="custom-loader m-auto"></div>


    <ul class="list js-list">

      <li v-for="country in countrys" :key="country" class="item">
      <img class="item__img js-img" :src="country.flag" alt="">
      <h3 class="item__title js-title">{{ country.name }}</h3>
      <p class="item__text js-text">Lorem ipsum dolor sit amet.</p>
      <span class="item__span population">Native-Name: {{ country.nativeName }}</span>
      <span class="item__span population">Population: {{ country.population }}</span>
      <span class="item__span capital">Capital: {{ country.capital }}</span>
      <span class="item__span region">Region: {{ country.region }}</span>
    </li>

    </ul>    
  </div>

</template>

<style lang="css" scoped>
.m-auto{
  margin: 15% auto;
}
.custom-loader {
  width: 150px;
  height: 150px;
  display: grid;
  border:8px solid #0000;
  border-radius: 50%;
  border-color:#E4E4ED #0000;
  animation: s6 1s infinite linear;
}
.custom-loader::before,
.custom-loader::after {    
  content:"";
  grid-area: 1/1;
  margin:4px;
  border:inherit;
  border-radius: 50%;
}
.custom-loader::before {
  border-color:#766DF4 #0000;
  animation:inherit; 
  animation-duration: .5s;
  animation-direction: reverse;
}
.custom-loader::after {
  margin:16px;
}

@keyframes s6 { 
  100%{transform: rotate(1turn)}
}

/* MODE STYLE */

:root{
  --text-light-color: #000;
  --text-dark-color: #fff;
}

.dark{
  background-color: #050505;
  color: var(--text-dark-color);
}

.item-textColor{
  color: var(--text-light-color);
}

/* MODE STYLE */

.wrap{
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 25px 0;
}

.box{
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.select{
  padding: 10px 20px;
  border-radius: 8px;
  border: none;
  margin-right: 20px;
}

.search{
  padding: 10px 20px;
  border: none;
  margin-right: 20px;
  border-radius: 8px;
}

.list{
  list-style-type: none;
  margin: 0;
  padding: 0;
  display: flex;
  justify-content: center; 
  flex-wrap: wrap;
  gap:  50px;
  align-items: center;
}

.mode{
  padding: 10px 20px;
  border: none;
  background-color: transparent;
}

.mode-img{
  width: 20px;
  height: 20px;
  background-color: transparent;
}

.item{
  padding-bottom: 20px;
  display: flex;
  flex-direction: column;
  /* justify-content: center; */
  /* align-items: center; */
  background-color: rgba(340, 345, 430, 0.5);
  border-radius: 8px;
  width: 300px;
  gap: 10px;
  /* margin: 0 10px 20px 0; */
  box-shadow: 0px 1px 12px 4px rgba(0,0,0,0.35);
-webkit-box-shadow: 0px 1px 12px 4px rgba(0,0,0,0.35);
-moz-box-shadow: 0px 1px 12px 4px rgba(0,0,0,0.35);
}

.item:last-child{
  margin: 0;
}

.item__img{
  width: 300px;
  height: 150px;
  object-fit: contain;
  object-position: center;
  border-top-left-radius: 8px;
  border-top-right-radius: 8px;
}

.item__title{
  margin: 0;
  margin: 20px 0;
  text-align: center;
}

.item__text{
  margin: 0;
  text-align: center;
}

.item__span{
  margin-top: 15px;
  margin-left: 20px;
}


</style>
