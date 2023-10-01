<script setup>

</script>

<template>
    
<ul class="ma-liste" style="background-color: transparent;">
  <li><a>Timer mode</a></li>
  <li><a class="active">Life mode</a></li>
  <li><a>Free play</a></li>
</ul>

</template>


<style>


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
</style>