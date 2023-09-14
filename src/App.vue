<template>
<div>
  <h1>Fish App</h1>
  <FishForum :fishData="fishData" />
    
  <h2>All fish in the database:</h2>
         <!-- List the fish data -->
  <table>
    <tr>
      <th>Fish name</th>
    </tr>
    <tr v-for="fish in fishData" :key="fish.id">
      <td>{{fish.name}}</td>
    </tr>
  </table>
</div>
</template>

<script lang="ts" setup>
import { defineComponent, ref, onBeforeMount } from 'vue';
import FishForum from './components/FishForum.vue';

interface Fish {
  name: string;
  id: number;
}


const fishData = ref<Fish[]>([]);

// Function to fetch fish data from your API
async function fetchFishData() {
  try {
    const response = await fetch('http://localhost:5069/fish-controller/get-fish');
    if (!response.ok) {
      throw new Error('Failed to fetch fish data');
    }
    const data = await response.json();
    console.log('Response:', data);

    fishData.value = data;
  } catch (error) {
    console.error(error);
  }
}

onBeforeMount(() => {
  // Make the API request before the component is mounted
  fetchFishData();
});

defineComponent({
  name: 'App',
  components: {
    FishForum,
  }
});
</script>






<style lang="scss" scoped>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

table {
  font-family: arial, sans-serif;
  border-collapse: collapse;
  width: 100%;
}

td, th {
  border: 1px solid #dddddd;
  text-align: left;
  padding: 8px;
}

tr:nth-child(even) {
  background-color: #dddddd;
}
</style>
