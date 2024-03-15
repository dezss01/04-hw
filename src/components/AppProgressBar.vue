<template>
  <div class="progress" role="progressbar" aria-valuemin="0" aria-valuemax="100">
    <div class="progress-bar" :style="this.progressBarWidth"></div>
  </div>
</template>

<script>
export default {
  props: {
    progressBarWidth: { required: true },
  },
};
</script>
