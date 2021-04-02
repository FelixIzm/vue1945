<template>
  <v-data-table
    :headers="headers"
    :items="desserts"
    :items-per-page="5"
    class="elevation-1 mytable table"
  ></v-data-table>
</template>

<style scoped >
  .mytable .v-table table {
    width: 100%;
    border: none;
    margin-bottom: 20px;
  }
  .mytable .v-table table thead th {
    font-weight: bold;
    text-align: left;
    border: none;
    padding: 10px 15px;
    background: #d8d8d8;
    font-size: 14px  !important;
  }
  .mytable .v-table table thead tr th:first-child {
    border-radius: 8px 0 0 8px;
  }
  .mytable .v-table table thead tr th:last-child {
    border-radius: 0 8px 8px 0;
  }
  .mytable .v-table table tbody td {
    text-align: left;
    border: none;
    padding: 10px 15px;
    font-size: 14px;
    vertical-align: top;
  }
  .mytable .v-table table tbody tr:nth-child(even) {
    background: #f3f3f3;
  }
  .mytable .v-table table tbody tr td:first-child {
    border-radius: 8px 0 0 8px;
  }
  .mytable .v-table table tbody tr td:last-child {
    border-radius: 0 8px 8px 0;
  }
</style>

<script>
export default {
  name: "tableunit",
  data() {
    return {
      headers: [
        {
          text: "Dessert (100g )",
          align: "start",
          sortable: false,
          value: "name",
        },
        { text: "Calories", value: "calories" },
      ],
      desserts: [],
    };
  },
};
</script>
