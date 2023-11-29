<template>
  <div id="app">
    <h1>Генератор шуток</h1>
    <button @click="getSetup()">получить </button>
    <div v-if="res != null">
    <h3>{{showsetup}}</h3>
    <h3> {{showPunch}}</h3>
  </div>
</div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'App',
  data(){ 
    return{
      punchline: '',
      setup: '',
      res: null
    }
  },
  computed:{
    showsetup(){
      return 'Заход: ' + this.res.setup
    },
    showPunch(){
      return 'Добив: ' + this.res.punchline

    }
  },
  methods: {
    getSetup(){
      axios
      .get('https://official-joke-api.appspot.com/random_joke')
      .then((data) => (this.res = data.data))
      .then((result) => (console.log(result)))
    }
  }
}
</script>

<style>
body {
	background: linear-gradient(90deg, #9483c7, #1100ff, #23a6d5, #23d5ab);
	background-size: 400% 400%;
	animation: gradient 10s ease infinite;
	transform: translate3d(0, 0, 0);
  font-size: 35px;
  color: white;
}
 
@keyframes gradient {
	0% {
		background-position: 0% 50%;
	}
	50% {
		background-position: 100% 50%;
	}
	100% {
		background-position: 0% 50%;
	}
}
#app{
  width: 60%;
  height: 500px;
  background-color:rgba(0, 0, 0, 0.6);
  border-radius: 20px;
  text-align: center;
  padding: 50px;
  margin: 50px auto;
}

button{
  padding: 10px 15px;
  border: none;
  outline: none;
  font-family: Arial, Helvetica, sans-serif;
  font-size: 20px;
  color: white;
  background-color: orange;
  border-radius: 10px;
  transition: all 1s;
}

/*анимация */

button:hover{
  background-color: #9483c7;
  transform: scale(1.6);
}
h1{
  animation: text 5s ease;
}
@keyframes text{
  0%{
    opacity: 0;
    transform: translateY(-400px);
  }
  100%{
    opacity: 1;
    transform: translateY(0px);
  }
}
h3{
  animation: joke 1s ease;
}
@keyframes joke{
  0%{
    opacity: 0;
    transform: rotateZ(0);
  }
  100%{
    opacity: 1;
    transform: rotateZ(1440deg);
    }
}
</style>
