<template>

<div className="input-container" >
    <label ><b>Get Fish by ID
    <input
    type="text" 
    placeholder="Enter fish name" 
    v-model="getFishId"
    name="Last_name" 
    required />
    </b></label>
    <AddFish :buttonColor="parentColor" :buttonText="parentText" @click="getFishById" />
</div>
 
 <div className="input-container" >
    <label ><b> Delete Fish by ID
    <input
    type="text" 
    placeholder="Enter fish name" 
    name="Last_name" 
    v-model="deleteFishId"
    required />
    </b></label>
    <AddFish :buttonColor="parentColor" :buttonText="parentText" @click="deleteFishById" />
</div>
 <div className="input-container" >
    <label ><b>Add Fish by ID
    <input
    type="text" 
    placeholder="Enter fish name" 
    name="Last_name" 
    v-model="addFishId"
    required />
    </b></label>
    <AddFish :buttonColor="parentColor" :buttonText="parentText" @click="addFishById"/>
</div>
<div className="input-container" >
    <label ><b>Update Fish by ID
    <input
    type="text" 
    placeholder="Enter fish name" 
    name="Last_name"
    v-model="updateFishId"
    required />
    </b></label>
    <AddFish :buttonColor="parentColor" :buttonText="parentText" @click="updateFishById" />
</div>

   
</template>

<script setup lang="ts">
import { defineComponent, ref, onBeforeMount } from 'vue';
import AddFish from './AddFish.vue';
import axios from 'axios';


interface Fish {
  name: string;
  id: number;
}

//AddFishButton properties
const parentColor = "aqua";
const parentText = "Send request";

let getFishId =ref('')
let deleteFishId =ref('')
let addFishId =ref('')
let UpdateFishId =ref('')



const fishData = ref<Fish | null>(null);

async function getFishById() {
  try {
    const response = await fetch(`http://localhost:5069/fish-controller/get-fish/${getFishId.value}`);
    if (!response.ok) {
      throw new Error('Failed to fetch fish data');
    }
    const data = await response.json();
    console.log('Response:', data);
  console.log('Input Value:', getFishId.value);

    fishData.value = data;
  } catch (error) {
    console.error(error);
  }
}

async function deleteFishById() {
  try {
    const response = await fetch(`http://localhost:5069/fish-controller/delete-fish/${deleteFishId.value}`);
    if (!response.ok) {
      throw new Error('Failed to fetch fish data');
    }
    const data = await response.json();
    console.log('Response:', data);
  console.log('Input Value:', deleteFishId.value);
  } catch (error) {
    console.error(error);
  }
}




</script>



<style lang="sass" scoped>

</style>
