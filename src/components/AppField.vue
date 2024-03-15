<template>
  <div class="form-group">
    <label>
      {{ label }}
      <span v-if="activated" :class="checkedClass">
        <font-awesome-icon :icon="fontAwesomeCheckedClass" />
      </span>
    </label>
    <input type="text" class="form-control" :value="value" @input="onInput" />
  </div>
</template>

<script>
export default {
  props: {
    label: { type: String, required: true },
    value: { type: String, required: true },
    valid: { type: Boolean, required: true },
  },
  data() {
    return {
      activated: this.value != "",
    };
  },
  methods: {
    onInput(e) {
      this.activated = true;
      this.$emit("updated", e.target.value);
    },
  },
  computed: {
    fontAwesomeCheckedClass() {
      return this.valid ? "fa fa-check-circle" : "fa fa-exclamation-circle";
    },
    checkedClass() {
      return this.valid ? "text-success" : "text-danger";
    },
  },
};
</script>
