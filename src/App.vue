<template>
  <div id="app" class="kletka">
    <Table />
  </div>
</template>

<script>
import Table from "./components/Table.vue";

export default {
  components: {
    Table,
  },
};
</script>
<style>
.kletka {
  background: linear-gradient(#bbb, transparent 1px),
    linear-gradient(90deg, #bbb, transparent 1px);
  background-size: 20px 20px;
  background-position: center center;
  min-height: 100vh;
}
</style>
