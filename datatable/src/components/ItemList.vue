<template>
  <div>
    <h1>Data Table</h1>
    <div class="mt-5">
      <select name="" id="" v-model="selected" @change="sortStatus()" class="border-2 mb-5 rounded h-10 p-2 ml-5 text-black">
        <option class="p-2" value="" >FILTER BY STATUS</option>
        <option v-for="(status, index) in listStatus" v-bind:key="index" 
            >{{ status }}</option>
      </select>

      <select name="" id="" v-model="selectedOfferType" @change="sortOfferType()" class="border-2 mb-5 rounded h-10 p-2 ml-5 text-black">
        <option class="p-2" value="" >FILTER BY OFFER TYPE</option>
        <option v-for="(offerType, index) in listOfferType" v-bind:key="index">{{ offerType }}</option>
      </select>

      <button
        class="border-2 mb-5 rounded  p-2 ml-5 bg-red-600 text-white"
        @click="onReset"
        >CLEAR ALL FILTER
      </button>
      
    </div>

    <table>
      <tr class="text-blue-400 text-xl">
        <th @click="sortList('name')">Name &#8597;</th>
        <th @click="sortList('identifier')">Identifier &#8597;</th>
        <th @click="sortList('id')">Id &#8597;</th>
        <th @click="sortList('created')">Created &#8597;</th>
        <th @click="sortList('display_count')">Display-count &#8597;</th>
        <th @click="sortList('offer_type')">Offer-type &#8597;</th>
        <th @click="sortList('status')">Status &#8597;</th>
      </tr>
      <tr v-for="(data, index) in sortedData" :key="index">
        <td>{{ data.name }}</td>
        <td>{{ data.identifier }}</td>
        <td>{{ data.id }}</td>
        <td>{{ data.created }}</td>
        <td>{{ data.display_count }}</td>
        <td>{{ data.offer_type }}</td>
        <td :style="data.status==='offline' ? 'background:blue;text-align:center': 'background:green;text-align:center'">
          {{ data.status }}
        </td>
      </tr>
    </table>
  </div>
</template>

<script>

import rawData from "../../public/data.json";

export default {
  name: "ItemList",
  computed: {
    originalData() {
      return rawData
    }
  },
  data() {
    return {
      sortedData: [],
      sortedbyASC: true,
      listStatus: ['online', 'offline'],
      selected: '',
      listOfferType: ['Fall', 'Winter','-' ],
      selectedOfferType: '',
    };
  },
  mounted() {
    this.sortedData = this.originalData;
  },
  methods: {
    sortList(sortBy) {
      if (this.sortedbyASC) {
        this.sortedData.sort((x, y) => (x[sortBy] > y[sortBy] ? -1 : 1));
        this.sortedbyASC = false;
      } else {
        this.sortedData.sort((x, y) => (x[sortBy] < y[sortBy] ? -1 : 1));
        this.sortedbyASC = true;
      }
    },
    sortStatus () {
      this.sortedData = this.originalData;
      if(this.selected){
        this.sortedData = this.sortedData.filter(
        (row) => row= row.status === this.selected
      )
      }else{
        this.sortedData = this.originalData;
      }   
    },
    sortOfferType () {
      this.sortedData = this.originalData;
      if(this.selectedOfferType){
      this.sortedData = this.sortedData.filter(
        (row) => row= row.offer_type === this.selectedOfferType
      )
      }else{
        this.sortedData = this.originalData;
      } 
    },
    onReset () {
      this.sortedData = this.originalData;
      this.selected = '';
      this.selectedOfferType = '';
    }
  },
};
</script>

<style>
h1{
  font-size: 36px;
    text-align: center;
    text-decoration: underline;
}

table {
  font-family: arial, sans-serif;
  border-collapse: collapse;
  width: 100%;
}

td,
th {
  border: 1px solid #dddddd;
  text-align: left;
  padding: 8px;
}

th:hover {
  cursor: pointer;
  background: yellowgreen;
}

tr:nth-child(even) {
  background-color: grey;
}
</style>