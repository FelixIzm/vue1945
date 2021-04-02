<template>
  <div class="home">
    <form @submit.prevent="sendData">
      <div class="form-control">
        <label for="unit">Воинское подразделение</label>
        <input v-model="unit" id="unit" type="text" />
      </div>
      <div class="form-control">
        <label for="period">Период выборки</label>
        <date-picker
          v-model="period"
          ref="datePicker"
          name="contract_period"
          range
          format="DD-MM-YYYY"
          valueType="format"
          confirm
          width="100%"
        ></date-picker>
      </div>

      <input type="submit" class="send" value="Send" />
      <!--
      <div id="textExample">
        <table class="table table-bordered">
          <thead>
            <tr>
              <th v-for="column in tableColumns" v-bind:key="column.title">
                {{ column.title }}
              </th>
            </tr>
          </thead>
          <tbody is="transition-group" name="user-list">
            <tr v-for="doc in docs" v-bind:key="doc._id">
                    <td> {{ doc['_source']['archive'] }} </td>
                    <td> {{ doc['_source']['archive'] }} </td>
                    <td> {{ doc['_source']['archive'] }} </td>
            </tr>
          </tbody>
        </table>
      </div>
      <div id="info">
        {{ info }}
      </div>
      -->
      <tableunit ref="tableunit" ></tableunit>
    </form>
  </div>
</template>

<script>
import DatePicker from "vue2-datepicker";
import "vue2-datepicker/index.css";
import "vue2-datepicker/locale/ru";
import axios from "axios";
//import Vuetify from 'vuetify';
import Vue from "vue";
import Vuetify from "vuetify";
Vue.use(Vuetify);

import tableunit from "@/components/TableUnit_copy.vue";
//import tableunit from "@/components/TableUnit.vue";
//import TableUnit from '../components/TableUnit.vue';

export default {
  components: { DatePicker, tableunit},
  data() {
    return {
      //period: [new Date(String('08-01-2019')), new Date(String('08-30-2019'))],
      //period: [new Date(2019, 7, 1), new Date(2019, 7, 30)],
      period: [],
      docs:[],
      unit: "147 сд",

      //tableunit: "dfg"
    };
  },
  methods: {
    sendData() {
      //this.tableunit = tableunit;
      this.docs = [];
      console.log(this.unit, this.period);
      //this.$refs.tableunit.desserts = [];
      axios
        .get("http://localhost:8000/unit/:rdf/:dd")
        //.then((response) => (this.info = response.data[0]['_source']['archive']));
        //.then((response) => (this.docs = response.data))
        //.then(function (docs) { this.docs = docs })
        .then((response)=> {
              response.data.forEach((element) => {
                let item = {};
                item.name =element['_id'];
                item.calories = element['_source']['authors'];
                this.$refs.tableunit.desserts.push(item);
                //console.log(element);
              })
              console.log(this.$refs.tableunit.desserts);
        })

        
    },
  },

  mounted() {
    //this.$refs.tableunit = tableunit;
    this.$refs.datePicker.currentValue = [
      new Date(String("01-01-1939")),
      new Date(String("12-31-1946")),
    ];
  },
};
</script>

<style>
.form-control {
  padding: 5px;
}
.form-control label {
  display: block;
}
.send {
  margin: 5px;
}
</style>
