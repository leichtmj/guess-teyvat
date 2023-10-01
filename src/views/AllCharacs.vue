<script setup>
    import Table from '../components/Table.vue';
    import data from '../assets/data.json'

</script>

<template>


  <div class="overflow-x-auto">
    <table class="table">
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
      <tbody v-for="d in data">
        <Table :name="d.name" :quality="d.quality" :element="d.element" :weapon="d.weapon" :region="d.region" :modeltype="d.modeltype" :avatar="d.avatar"></Table>
      </tbody>
      
    </table>
  </div>
</template>