<template>
  <div class="container mt-2">
    <form v-if="!showResultTable" @submit.prevent="sendForm">
      <div>
        <app-field
          v-for="(field, i) in info"
          :key="i"
          :label="field.label"
          :value="field.value"
          :valid="field.valid"
          @updated="onUpdate(i, $event)"
          class="mb-4"
        />
      </div>
      <app-progress-bar :current="fieldsDone" :max="info.length" class="mb-3" />
      <!-- {{ fieldsDone }}
      {{ formReady }}
      {{ progressStyles }} -->
      <button class="btn btn-primary" :disabled="!formReady" type="submit">
        Send Data
      </button>
    </form>
    <div v-else>
      <app-result-table :resultTable="this.info" />
    </div>
  </div>
</template>

<script>
import AppField from "./components/FieldPage.vue";
import AppProgressBar from "./components/ProgressBar.vue";
import AppResultTable from "./components/ResultTable.vue";

export default {
  components: {
    AppField,
    AppProgressBar,
    AppResultTable,
  },
  data: () => ({
    info: [
      {
        label: "Name",
        value: "",
        pattern: /^[a-zA-Z ]{2,30}$/,
      },
      {
        label: "Phone",
        value: "",
        pattern: /^[0-9]{7,14}$/,
      },
      {
        label: "Email",
        value: "",
        pattern: /.+/,
      },
      {
        label: "Some Field 1",
        value: "",
        pattern: /.+/,
      },
      {
        label: "Some Field 2",
        value: "",
        pattern: /.+/,
      },
    ],
    showResultTable: false,
  }),
  computed: {
    fieldsDone() {
      // return this.info.reduce((total, field) => total + (field.valid ? 1 : 0), 0)
      return this.info.filter((field) => field.valid).length;
    },
    formReady() {
      return this.fieldsDone >= this.info.length;
    },
    progressStyles() {
      let rel = (this.fieldsDone / this.info.length) * 100;
      return { width: rel + "%" };
    },
  },
  methods: {
    onUpdate(i, val) {
      let field = this.info[i];
      field.value = val.trim();
      field.valid = field.pattern.test(field.value);
    },
    sendForm() {
      if (this.formReady) {
        this.showResultTable = !this.showResultTable;
      }
    },
  },
  created() {
    this.info.forEach((field) => {
      field.valid = false;
      field.activated = false;
    });
  },
};
</script>
./components/Field.vue./components/ProgressBar.vue./components/ResultTable.vue./components/FieldPage.vue
