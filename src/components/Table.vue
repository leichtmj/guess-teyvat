<script setup>

import {ref, onMounted, onUpdated} from 'vue'
const emit = defineEmits(['emitValue']);

const props = defineProps({
        name: {
            type: String,
            required: true
        },
        quality: {
            type: String,
            required: true,
        },
        element: {
            type: String,
            required: true
        },
        weapon: {
            type: String,
            required: true
        },
        region: {
            type: String,
            required: true
        },
        modeltype: {
            type: String,
            required: true
        },
        avatar: {
            type: String,
            required: true
        },
        answer: {
            type: Array,
            required: true
        },
        data: {
          type:Array,
          required: true
        }
    })

console.log(props.answer)

onMounted(()=>{
  verif()
})

onUpdated(()=> {
  verif()
})

const coloration = (property, element) => {
    
  if(property==='name') {
    let e = document.querySelectorAll('tr')
    e[e.length-1].classList.add('green')
  }
  else {
    let e = document.querySelectorAll('td')
    e.forEach(el => {
      if (el.className===element[property]) {
        el.classList.add('green')
      }
    })
  }
}

const verif = () => {

  props.data.forEach(element => {
    
  if(props.answer['name']===element['name']) {
    console.log('gagné')
    coloration('name', element)
    emit('showGG',true)
    let tr = document.querySelectorAll('tr')
    emit('nbtry', tr.length-1)
  }

  if(props.answer['quality']===element['quality']) {
      coloration('quality', element)
      emit('showGG',false)
  }
  if(props.answer['element']===element['element']) {
      coloration('element', element)
      emit('showGG',false)
  }
  if(props.answer['weapon']===element['weapon']) {
      coloration('weapon', element)
      emit('showGG',false)
  }
  if (props.answer['region']===element['region']){
      coloration('region', element)
      emit('showGG',false)
  }
  if (props.answer['modeltype']===element['modeltype']){
      coloration('modeltype', element)
      emit('showGG',false)
  }
  });
  
}



</script>

<template>




          <!-- row 1 -->
          <tr>
            <td>
              <div class="flex items-center space-x-3">
                <div class="avatar">
                  <div class="mask mask-squircle w-12 h-12">
                    <img :src="avatar" alt="Avatar Tailwind CSS Component" />
                  </div>
                </div>
                <div :class="name">
                  {{ name }}
                </div>
              </div>
            </td>
            <td :class="quality">
                
              <img :src="`./src/assets/images/stars/${quality}.png`" alt="">
            </td>
            <td :class="element">
                <span>{{ element }}<img  :src="`./src/assets/images/elements/${element}.png`" alt=""></span>
            </td>
            <td :class="weapon">
               <span>{{ weapon }}<img :src="`./src/assets/images/weapons/${weapon}.png`" alt=""></span>
            </td>
            <td :class="region">
               <span>{{ region }}<img v-if="region!='None'" style="height: 25px;" :src="`./src/assets/images/regions/${region}.png`" alt=""></span>
            </td>
            <td :class="modeltype">
              {{ modeltype }}
            </td>
          </tr>
</template>

<style>
.red {
  background-color: red;
}

.green {
  background-color: green;
}

.blur {
backdrop-filter: blur(5px);
}

</style>