<script setup>

import {FontAwesomeIcon} from "@fortawesome/vue-fontawesome";
import { faSquarePlus} from "@fortawesome/free-regular-svg-icons";
import {faMinus} from "@fortawesome/free-solid-svg-icons";

const props = defineProps({
  count: { type: Number, required: true },
  minCount: { type: Number, required: true },
  maxCount: { type: Number, required: true }
})

const emit = defineEmits(['plusCount', 'minusCount'])
</script>

<template>
  <button class="btn btn-danger btn-sm" @click="$emit('minusCount')">
    <FontAwesomeIcon :icon="faMinus" class=""/>
  </button>
  <input type="text" name="" id="" class="mx-2" :value="count">
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