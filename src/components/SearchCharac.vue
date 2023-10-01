<script setup>

import {ref} from 'vue';

const props = defineProps({
        data: {
            type: Array,
            required: true
        },
    })

let data_names=[]

let data = props.data
console.log(data)

data.forEach(element => {
    data_names.push(element.name)
});

console.log(data_names)

const createHTML = (tag, parent, text=null, classs=null, id=null) => {
	let element = document.createElement(tag)
	if (text)
		element.appendChild(document.createTextNode(text))
	parent.appendChild(element)
	if (classs)
		element.classList.add(classs)
	if (id)
		element.id = id
	return element
}


const autocompleteMatch = (input) => {

    console.log('autofunc')
    console.log(input)
    if (input == '') {
        return [];
    }
    // console.log(data_names)
    var reg = new RegExp(input.toLowerCase())
  
    return data_names.filter(function(term) {
	    if (term.toLowerCase().match(reg)) {
  	        return term;
	    }
    });
}

const test = () => {
    console.log('coucou')
}

const submitName = (event) => {
    if(event.keyCode=== 'Enter') {
        console.log('ok')
    }
}


const showResults = (val) => {

  console.log(val)
  let res = document.getElementById("result");

  res.innerHTML = '';
  let list = '';

  let terms = autocompleteMatch(val);

  let ul = createHTML('ul', res)
  for (let i=0; i<terms.length; i++) {
    let li = createHTML('li', ul, terms[i])
    li.addEventListener('click', test)
    li.addEventListener('keydown', submitName)
  }
}

</script>

<template>


<div class="join join-vertical lg:join-horizontal ">
    <input type="text" class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-auto p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" @keyup="showResults($event.target.value)">
    <button class="btn">Valider</button>
</div>
        

    
        <div id="result"></div>

</template>