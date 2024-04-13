<template>
  <TheNav />
  <div class="container">
    <TheTable :data="data"/>
  </div>
</template>

<script setup>
import TheNav from "./components/TheNav.vue";
import TheTable from "./components/TheTable.vue";
import {data} from "./data.js";


</script>