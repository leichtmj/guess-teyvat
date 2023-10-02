<template>
    <div class="position">
      <h1 class="white">Timer Mode</h1>
      <h1 class="white" >Compte à rebours: {{ formatTime }}</h1>
      <ul>
        <li v-if="!countdownRunning">
            <button class="white" @click="startCountdown"  >Démarrer</button>
        </li>
        <li v-if="countdownRunning">
            <button class="white" @click="stopCountdown" >Arrêter</button>
        </li>
        <li v-if="countdownRunning">
            <button class="white" @click="resetCountdown" >Réinitialiser</button>
        </li>
      </ul>
    </div>
  </template>
  
  <script setup>
  import { ref, computed, watch, onBeforeUnmount } from 'vue';
  
  const initialTime = 60; // Temps initial en secondes
  const seconds = ref(initialTime);
  const countdownRunning = ref(false);
  let countdownIntervalId = null;
  
  
  const formatTime = computed(() => {
    const minutes = Math.floor(seconds.value / 60);
    const remainingSeconds = seconds.value % 60;
    return `${minutes.toString().padStart(2, '0')}:${remainingSeconds.toString().padStart(2, '0')}`;
  });
  
  const startCountdown = () => {
      if (!countdownRunning.value) {
          countdownRunning.value = true;
          countdownIntervalId = setInterval(() => {
              if (seconds.value > 0) {
                  seconds.value--;
                } else {
                    stopCountdown();
                }
            }, 1000);
        }
  };
  
  const stopCountdown = () => {
      if (countdownRunning.value) {
          countdownRunning.value = false;
          clearInterval(countdownIntervalId);
        }
  };
  
  const resetCountdown = () => {
      countdownRunning.value = false;
      clearInterval(countdownIntervalId);
      seconds.value = initialTime;
    };
  
  onBeforeUnmount(() => {
    // Nettoyer l'intervalle lorsque le composant est détruit
    clearInterval(countdownIntervalId);
  });
  
  </script>

<style>
.white {
    color: white;
    margin-top: 5px;
}

.cursor {
    cursor: no-drop;
}

.position {
    position: absolute;
    left: 80%;
    top: 11%;
    backdrop-filter: blur(5px);
    padding: 10px 10px 10px 10px;
}

</style>