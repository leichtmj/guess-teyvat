<script setup>
  import {ref,computed, watch, onBeforeUnmount} from 'vue'
  import Table from '../components/Table.vue';
  import data from '../assets/data.json'
  import SearchBar from '../components/SearchBar.vue';
  import Countdown from '../components/Countdown.vue';
  import LifeMode from '../components/LifeMode.vue';
  
  const selectedcharac = ref('')
  const showGG = ref('')
  const nbtry = ref('')

  let array_answers = []
  
  const getselectedcharac = (e) =>{
    selectedcharac.value=e
    array_answers.push(e)
  }

  const getNbTry = (e) => {
    nbtry.value=e
  }

  const getShowGG = (e) => {
    showGG.value=e
  }
  const answer = data[Math.floor(Math.random() * data.length)];
  
  //Timer
  const seconds = ref(0);
  const timerRunning = ref(false);
  let intervalId = null;
  const formatTime = computed(() => {
    const minutes = Math.floor(seconds.value / 60);
    const remainingSeconds = seconds.value % 60;
    return `${minutes.toString().padStart(2, '0')}:${remainingSeconds.toString().padStart(2, '0')}`;
  });
  const startTimer = () => {
    if (!timerRunning.value) {
      timerRunning.value = true;
      intervalId = setInterval(() => {
        seconds.value++;
      }, 1000);
    }
  };
  const stopTimer = () => {
    if (timerRunning.value) {
      timerRunning.value = false;
      clearInterval(intervalId);
    }
  };
  const resetTimer = () => {
    timerRunning.value = false;
    clearInterval(intervalId);
    seconds.value = 0;
  };
  
  onBeforeUnmount(() => {
    // Nettoyer l'intervalle lorsque le composant est détruit
    clearInterval(intervalId);
  });

  let showTimeMode = ref(false)
  let showLifeMode = ref(false)
  let showFreeMode = ref(true)


  const openTimeMode =() => {
    showTimeMode.value=true
    showLifeMode.value=false
    showFreeMode.value=false
  }

  
  const openLifeMode =() => {
    showTimeMode.value=false
    showLifeMode.value=true
    showFreeMode.value=false
  }

  const openFreeMode =() => {
    showTimeMode.value=false
    showLifeMode.value=false
    showFreeMode.value=true
  }

</script>

<template>

<Countdown v-if="showTimeMode"></Countdown>
<LifeMode v-if="showLifeMode" ></LifeMode>

<ul class="ma-liste" style="background-color: transparent;">
  <li><a @click="openTimeMode">Timer mode</a></li>
  <li><a @click="openLifeMode">Life mode</a></li>
  <li><a @click="openFreeMode">Free play</a></li>
</ul>

<div>
    <h1>Timer: {{ formatTime }}</h1>
    <button @click="startTimer" :disabled="timerRunning">Start</button>
    <button @click="stopTimer" :disabled="!timerRunning">Stop</button>
    <button @click="resetTimer" :disabled="!timerRunning && seconds === 0">Reset</button>
  </div>

<h1 style="font-size: 25px; display: flex; justify-content: center; margin-top: 0.5%; color: white;">Guess the character !</h1>


<SearchBar @selectedcharac="getselectedcharac"></SearchBar>

<p style="display: none;">Variable reçue : {{ selectedcharac }}</p>

  <div>
    <table class="max-w-screen-md mx-auto table">
      <!-- head -->
      <thead>
        <tr>
          <th>Name</th>
          <th>Quality</th>
          <th>Element</th>
          <th>Weapon</th>
          <th>Region</th>
          <th>Model type</th>
        </tr>
      </thead>
      <tbody v-for="d in array_answers">
        <Table @showGG="getShowGG" @nbtry="getNbTry" :name="d.name" :quality="d.quality" :element="d.element" :weapon="d.weapon" :region="d.region" :modeltype="d.modeltype" :avatar="d.avatar" :data="array_answers" :answer="answer"></Table>
      </tbody>
      
    </table>
  </div>

  <div v-if="showGG" class="card w-100 bg-base-100 shadow-xl absolute top-1/2 left-1/2 transform -translate-x-1/2 -translate-y-1/2">
            <div class="card-body">
              <h2 class="card-title text-white">Well done !</h2>
              <p class="text-white">You guess correctly in {{ nbtry }} times !</p>
              <p class="text-white">Time elapsed : {{  }}</p>
              <div class="card-actions justify-end">
                <a href="/"><button class="btn btn-primary">Retry</button></a>
              </div>
            </div>
          </div>
</template>

<style>

.blur {
backdrop-filter: blur(5px);
}

table {
  background-color: white;
}

th {
  font-size: 15px;
}


.ma-liste {
  max-width: 150px;
  list-style: none;
  padding: 0;
  backdrop-filter: blur(5px);
  margin-left: 12%;
  position: absolute;
  top: 10%;
}

.ma-liste li {
  max-width: 150px;
  padding: 10px;
  cursor: pointer;
  transition: background-color 0.3s;
  color: white;
  border-radius: 15px 15px 15px 15px;
}

.ma-liste li:hover {
  background-color: lightgray; 
}

.show-gg {
  position: absolute;
  width: auto;
  left: 50%;
}

</style>