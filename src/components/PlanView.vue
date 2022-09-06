<template>
  <div class="about">
    <h1 align="center">{{ msg }}</h1>
    <v-form>
      <v-container>
        <v-row> </v-row>
        <v-row>
          <v-col cols="4" sm="5" md="5">
            <v-slider
              v-model="fx5.val"
              :color="fx5.color"
              :label="fx5.label"
              min="10"
              max="700"
              thumb-label="always"
            ></v-slider>

            <v-slider
              v-model="fx6.val"
              :label="fx6.label"
              :color="fx6.color"
              min="10"
              max="700"
              thumb-label="always"
            ></v-slider>
          </v-col>
          <v-spacer></v-spacer>
          <v-col cols="4" sm="5" md="5">
            <v-slider
              v-model="fx7.val"
              :label="fx7.label"
              min="10"
              max="700"
              :color="fx7.color"
              thumb-label="always"
            ></v-slider>
            <v-slider
              v-model="fx8.val"
              :label="fx8.label"
              min="10"
              max="700"
              :color="fx8.color"
              thumb-label="always"
            ></v-slider>
            <v-slider
              v-model="fx9.val"
              :label="fx9.label"
              min="1"
              max="95"
              :color="fx8.color"
              thumb-label="always"
            ></v-slider>
            <v-slider
              v-model="fx10.val"
              :label="fx10.label"
              min="1"
              max="15"
              :color="fx8.color"
              thumb-label="always"
            ></v-slider>
            <v-slider
              v-model="fx11.val"
              :label="fx11.label"
              min="1"
              max="15"
              :color="fx8.color"
              thumb-label="always"
            ></v-slider>
          </v-col>
        </v-row>
      </v-container>
      <div class="text-center">
        <v-btn rounded color="primary" dark @click="updateCarbon"
          >Update Carbon Footprint</v-btn
        >
        <v-btn color="primary" href="https://ecologi.com/" target="_blank" text>
          <span class="mr-2">Plant a tree </span>
          <v-icon>mdi-open-in-new</v-icon>
        </v-btn>
      </div>
    </v-form>
  </div>
</template>
<script>
//local registration
/* eslint-disable */
import Airtable from 'airtable';
import axios from "axios";
import CarbonGraph from "../components/CarbonGraph";
import mondaySdk from "monday-sdk-js";
const monday = mondaySdk();



export default {
  name: "PlanView",
  props: {
    //rows: rows,
    msg: String,
  },
  //component code
  data() {
    return {
      companyName: "",
      requestor: "",
      description: "approval",
      item: [],
      done: "success",
      settings: null,
      context: undefined,
      fx5: { label: "Monthly power $", val: 75, color: "green lighten-1'" },
      fx6: { label: "Monthly gas  $", val: 80, color: "green lighten-1'" },
      fx7: { label: "Monthly car miles #", val: 5, color: "green lighten-1'" },
      fx8: { label: "Monthly flights ", val: 50, color: "#234560" },
      fx9: { label: "Volunteers #", val: 50, color: "#234560" },
      fx10: { label: "Vegan diet", val: 5, color: "green lighten-1'" },
      fx11: { label: "Trees planted #", val: 5, color: "green lighten-1'" },
    };
  },
  mounted: function () {
    //this.loadPlan();
  },
  methods: {

   updateCarbon(){
      var power = this.fx5.val;
      var gas = this.fx6.val;
      var flights = this.fx8.val;
      var miles = this.fx7.val;
      var vega =this.fx10.val; 

   const variables = ({
    boardId : 3186810139,
    groupId: "topics",
    itemName : "New Item",
    columnValues: JSON.stringify({
        numbers: gas,
        numbers_15: power,
        numbers_10: miles,
        numbers_1: flights,
        dup__of_monthly_flights:vega,
        text: "Yose Sam",
    })
    });

   const query = `mutation create_item ($boardId: Int!, $groupId: String!, $itemName: String!, $columnValues: JSON!) { 
    create_item (
        board_id: $boardId,
        group_id: $groupId,
        item_name: $itemName, 
        column_values: $columnValues
    ) 
    { 
        id
    } 
    }`;
     monday.api(query,{variables}).then((res) => {
      console.log('new item info: ', res);
   
   });
    alert('updated');
   },

    updateCarbon1(){
     alert('hello');
      let query5 = 'mutation ($myItemName: String!, $columnVals: JSON!) { create_item (board_id:3186810139, item_name:$myItemName, column_values:$columnVals) { id } }';
        let vars = {
          "myItemName" : "Hello, world!",
          "columnVals" : JSON.stringify({
            "Status" : {"label" : "Done"},
            "Monthly miles" : {"numbers" : 100}
          })
        };

        fetch ("https://api.monday.com/v2", {
          method: 'post',
          headers: {
            'Content-Type': 'application/json',
            'Authorization' : 'eyJhbGciOiJIUzI1NiJ9.eyJ0aWQiOjE3NzY3Mjg3MCwidWlkIjozMTU0NzE5NiwiaWFkIjoiMjAyMi0wOC0yNlQxNDoyOTo1Ni4wMDBaIiwicGVyIjoibWU6d3JpdGUiLCJhY3RpZCI6MTI1Nzg0NDIsInJnbiI6InVzZTEifQ.dJqhXVLdY1yvpl0x_yADidBgh19NLEZmMiunKQc3N40'
          },
          body: JSON.stringify({
            'query' : query5,
            'variables' : JSON.stringify(vars)
          })
        })
          .then(res => res.json())
          .then(res => console.log(JSON.stringify(res, null, 2)));

    },
    

    sendMessage() {
      console.log("ok");

      var msg = this.description;
      var from = this.requestor;
      var em = this.email;

      var myHeaders = new Headers();
      myHeaders.append("Content-Type", "application/json");

      var graphql = JSON.stringify({
        query:
          "mutation sendEmail ($email: String,$requestor: String,$notes: String) {\n  insert_emails(email: $email, requestor: $requestor, notes: $notes) {\n    email\n    requestor\n    notes\n  }\n}",
        variables: { email: "em", requestor: "from", notes: "msg" },
      });
      var requestOptions = {
        method: "POST",
        headers: myHeaders,
        body: graphql,
        redirect: "follow",
      };

      fetch(
        "https://api.baseql.com/airtable/graphql/appneKtre6Ux4ESiq",
        requestOptions
      )
        .then((response) => response.text())
        .then((result) => console.log(result))
        .catch((error) => console.log("error", error));
    },
  },

   
  loadPlan: function () {
      console.log('name');
  },
  
};
</script>
<style>
nav a {
  font-weight: bold;
  color: #2c3e50;
}

</style>
