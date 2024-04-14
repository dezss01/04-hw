<script setup>

import {FontAwesomeIcon} from "@fortawesome/vue-fontawesome";
import {faSquarePlus} from "@fortawesome/free-regular-svg-icons";
import {faMinus} from "@fortawesome/free-solid-svg-icons";


const props = defineProps({
  count: { type: Number, required: true },
  minCount: { type: Number, required: true },
  maxCount: { type: Number, required: true }
})

const emit = defineEmits(['plusCount', 'minusCount', 'handleUpdateCount'])

const handleUpdateCount = (event) => {
  if(event.target.value > props.minCount && event.target.value < props.maxCount) {
    console.log('Значение инпута входит в диапазон')
  } else {
    console.log('По else')
  }
}
</script>

<template>
  <button class="btn btn-danger btn-sm" @click="$emit('minusCount')">
    <FontAwesomeIcon :icon="faMinus" class=""/>
  </button>
  <input :value="count" @input="(handleUpdateCount($event))" type="text" class="mx-2" >
  <button class="btn btn-success btn-sm" @click="$emit('plusCount')">
    <FontAwesomeIcon :icon="faSquarePlus" class=""/>
  </button>
  <div>
    <p>Count: {{ props.count }}</p>
    <p>MaxCount: {{ props.maxCount }}</p>
    <p>MinCount: {{ props.minCount }}</p>
  </div>

</template>

<style scoped>

</style>