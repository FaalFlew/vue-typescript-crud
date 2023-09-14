<template>
  <button
    class="add-to-cart button"
    aria-label="Add Fish to list"
    type="button"
    @click="fishRequest"
    :style="{ backgroundColor: props.buttonColor || undefined }">
    {{ buttonText }}
  </button>
</template>

<script setup lang="ts">
import { defineProps, defineEmits,ref } from 'vue';

const emits = defineEmits(['click'])

const props = defineProps({
  buttonColor: String,
  buttonText: String,
});


const fishRequest = () => {

  emits('click');
};

// create() {

// }
</script>

<style lang="sass" scoped>
/* Your scoped styles here */
</style>
