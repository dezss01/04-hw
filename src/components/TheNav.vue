<script setup>
import {faTruckFast} from "@fortawesome/free-solid-svg-icons/faTruckFast";
import {FontAwesomeIcon} from "@fortawesome/vue-fontawesome";
</script>

<template>
  <nav class="navbar navbar-expand-lg navbar-light bg-light">
    <div class="fw-bold font-monospace fs-2">SupperPupperStorage</div>
    <FontAwesomeIcon :icon="faTruckFast" class="fa-5x"/>
  </nav>
</template>
