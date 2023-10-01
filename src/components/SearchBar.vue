<script setup>
import data from '../assets/data.json';
import { ref, computed } from 'vue';

const search = ref('');
const emit = defineEmits(['emitValue']);
const data_names = data.map(element => element.name);

const toggleBorder = () => {
  if (search.value !== '') {
    const ul = document.querySelector('ul');
    ul.classList.add('border-up');
  }
};

const filteredList = computed(() => {
  return data_names.filter(item => {
    return (
      search.value && item.toLowerCase().includes(search.value.toLowerCase())
    );
  });
});

const validate = () => {
    let input = document.querySelector('input')
    let line = data.find((item) => item['name'] === input.value)
    console.log(line)
    emit('selectedcharac', line)
    input.value=''
}
const fill = (e) => {
    let input = document.querySelector('input')
    input.value=e.srcElement.innerHTML
}
</script>

<template>
    <main>
        <!-- <h1>Search a character...</h1> -->
        <div class="parent searchListMainDiv">
            <input placeholder='Select your character...' type="text" v-model="search" @input="toggleBorder" @keyup.enter="validate"/>
            <button class="btn child" style="color: white; margin-top: 13px; margin-left: 10px;" @click="validate" >Valider</button>
          
        <ul v-if="search" class="border-up">
            <li v-for="item in filteredList" @click="fill" :key="item">{{ item }}</li>
        </ul>
          
    </div>

    </main>
</template>



      <style>
  * {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
  }
  body {
    height: 100vh;
  }
  main {
    display: flex;
    justify-content: center;
    /* align-items: center; */
    /* height: 100vh; */
    width: auto;
  }

.parent {
    margin: 1rem;
  padding: 2rem 2rem;
  text-align: center;
}

.child {
    display: inline-block;
  padding: 1rem 1rem;
  margin-bottom: 1rem;
  vertical-align: middle;
}
.border-up {
    border: 1px solid rgb(255, 255, 255);
}


ul{
    margin: 0;
    padding: 0;
    list-style: none;
}

  .searchListMainDiv {
    min-width: 40%;
    margin: 0 1rem;
  }
    h1 {
    margin-bottom: 1rem;
  }
  .searchListMainDiv ul {
    list-style: none;
    padding: 0;
    margin: 0;
    margin-top: 0.5rem;
    box-shadow: 0px 0px 2px rgba(0, 0, 0, 0.25);
    max-height: 200px;
    overflow-y: auto;
  }
  .searchListMainDiv ul::-webkit-scrollbar {
    width: 5px;
  }
  .searchListMainDiv ul::-webkit-scrollbar-track {
    box-shadow: inset 0 0 5px #ddd;
    border-radius: 10px;
  }
  .searchListMainDiv ul::-webkit-scrollbar-thumb {
    background: rgb(183, 183, 183);
    border-radius: 10px;
  }
  .searchListMainDiv ul::-webkit-scrollbar-thumb:hover {
    background: #a2a2a2;
  }
  .searchListMainDiv input {
    background-image: url("https://imgur.com/0q2ec0d.png");
    background-size: 40px;
    background-repeat: no-repeat;
    background-position: 99% 50%;
    height: 45px;
    width: 80%;
    box-shadow: none;
    border: 1px solid #ddd;
    box-shadow: 0px 0px 15px rgba(0, 0, 0, 0.25);
    padding: 0 11.5rem 0 1rem;
    /* color: #333; */
    font-size: 18px;
  }
  .searchListMainDiv input:focus {
    border: 1px solid #ddd;
    outline: none;
  }
  .searchListMainDiv ul li {
    padding: 1.2rem 10px;
    font-size: 18px;
    font-weight: 500;
    line-height: 0;
    border-bottom: 1px solid #ddd;
    color: white;
    /* background-color: white; */
backdrop-filter: blur(5px);

    cursor: pointer;
  }
  .searchListMainDiv ul li:last-child {
    border: none;
  }
  </style>