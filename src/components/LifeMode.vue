<script setup>

const props = defineProps({
    isWon: Boolean,
    required:true
})



const lifes = 5

</script>

<template>
<div class="position">
    <h1 class="white">Life Mode</h1>
    <h1 class="white" >Lifes : {{ lifes }}</h1>
</div>
</template>

<style>

.white {
    color: white;
    margin-top: 5px;
}

.position {
    position: absolute;
    left: 80%;
    top: 11%;
    
}

</style>