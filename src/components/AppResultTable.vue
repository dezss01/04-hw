<template>
  <table class="table">
    <tbody>
      <tr v-for="(res, i) in this.resultTable" :key="i">
        <th scope="row">{{ i + 1 }}</th>
        <td>{{ res.label }}</td>
        <td>{{ res.value }}</td>
      </tr>
    </tbody>
  </table>
</template>

<script>
export default {
  props: {
    resultTable: { reqired: true },
  },
};
</script>
