

<template>
  <button class="btn btn-danger btn-sm" @click="removeCountByButton">
    <FontAwesomeIcon :icon="faMinus" class=""/>
  </button>
  <input :value="count" @input="handleUpdateCount" type="text" class="mx-2" >
  <button class="btn btn-success btn-sm" @click="addCountByButton">
    <FontAwesomeIcon :icon="faSquarePlus" class=""/>
  </button>
  <div>
    <p>Count: {{ props.count }}</p>
    <p>MaxCount: {{ props.maxCount }}</p>
    <p>MinCount: {{ props.minCount }}</p>
  </div>

</template>

<script setup>

import {FontAwesomeIcon} from "@fortawesome/vue-fontawesome";
import {faSquarePlus} from "@fortawesome/free-regular-svg-icons";
import {faMinus} from "@fortawesome/free-solid-svg-icons";


const props = defineProps({
  count: { type: Number, required: true },
  minCount: { type: Number, required: true },
  maxCount: { type: Number, required: true }
})

const emit = defineEmits(['update:count'])

const handleUpdateCount = (event) => {
  let result = Number(event.target.value)
  if(result < props.minCount) {
    result = props.minCount
  } else if(result > props.maxCount) {
    result = props.maxCount
  } else if(Number.isNaN(result)) {
    result = props.minCount
  }
  emit('update:count', result)
}
const addCountByButton = () => {
  if(props.count === 0) {
    emit('update:count', props.minCount)
  } else if(props.count < props.maxCount) {
    emit('update:count', props.count += 1)
  }
}
const removeCountByButton = () => {
  if(props.count > props.minCount) {
    emit('update:count', props.count -= 1)
  }
}

</script>

<style scoped>

</style>