<template>
  <div class="progress" role="progressbar" aria-valuemin="0" aria-valuemax="max">
    <div class="progress-bar" :style="styles"></div>
  </div>
</template>

<script>
export default {
  props: {
    current: { type: Number, required: true },
    max: { type: Number, default: 100 },
  },
  computed: {
    value() {
      return this.current / this.max;
    },
    styles() {
      return { width: this.value * 100 + "%" };
    },
  },
};
</script>
