<template>
  <v-form v-model="valid">
    <b-container fluid="md">
      <div class="container">
        <iframe
          :src="`http://127.0.0.1:1880/monitor/feed`"
          width="100%"
          height="1"
          frameborder="0"
        >
        </iframe>
      </div>
      <h1 align="left">{{ msg }}</h1>
      <h1 align="left"></h1>
      <div></div>
      <v-row>
        <v-col cols="4" sm="6" md="6">
          <v-slider
            v-model="fx9.val"
            :label="fx9.label"
            min="8"
            max="15"
            :color="fx9.color"
            thumb-label="always"
          ></v-slider>
        </v-col>
      </v-row>
      <v-row>
        <v-col cols="12" md="4">
          <v-text-field
            v-model="firstname"
            :rules="nameRules"
            :counter="10"
            label="Volunteering Feed Title"
            required
          ></v-text-field>
        </v-col>

        <v-col cols="12" md="4">
          <v-text-field
            v-model="lastname"
            :rules="nameRules"
            :counter="10"
            label="description"
            required
          ></v-text-field>
        </v-col>

        <v-col cols="12" md="4">
          <v-text-field
            v-model="email"
            :rules="emailRules"
            label="E-mail"
            required
          ></v-text-field>
        </v-col>
      </v-row>
      <v-row justify="space-around">
        <v-col class="d-flex" cols="12" sm="6">
          <v-date-picker
            v-model="picker"
            color="green lighten-1"
          ></v-date-picker>
        </v-col>
        <v-col class="d-flex" cols="12" sm="6">
          <v-select
            :items="items"
            label="Opprutunity Categories"
            dense
          ></v-select>
        </v-col>
      </v-row>
    </b-container>
    <div class="text-center">
      <v-btn rounded color="primary" dark @click="AddOppurtunity">Add </v-btn>
    </div>
  </v-form>
</template>

<script>
//import HelloWorld from "../components/PlanView";
//import HelloWorld from "../components/BnbDeal";
/* eslint-disable */ 
  export default {
    name: 'VolunteerOpp',

    components: {
  
    },
    props: {
    
    msg: String,
  },
  //component code
  data() {
    return {
      companyName: "",
      requestor: "",
      description: "approval",
      valid: false,
      firstname: '',
      lastname: '',
      value: '2',
      items: ['Multinationals', 'RIGHTS OF NATURE', 'ecocide', 'education','Climatologist','Biodiversity'],

      nameRules: [
        v => !!v || 'Name is required',
        v => v.length <= 10 || 'Name must be less than 10 characters',
      ],
      email: '',
      emailRules: [
        v => !!v || 'E-mail is required',
        v => /.+@.+/.test(v) || 'E-mail must be valid',
      ],
       picker: '2018-03-02',
        
      };
    },
     data: () => ({
      valid: false,
      firstname: '',
      lastname: '',
      value: '2',
      items: ['Multinationals', 'RIGHTS OF NATURE', 'ecocide', 'education','Climatologist','Biodiversity'],
      fx9: { label: "Reserved hours", val: 50, color: "#234560" },
      nameRules: [
        v => !!v || 'Name is required',
        v => v.length <= 10 || 'Name must be less than 10 characters',
      ],
      email: '',
      emailRules: [
        v => !!v || 'E-mail is required',
        v => /.+@.+/.test(v) || 'E-mail must be valid',
      ],
    }),
    methods: {
            
        AddOppurtunity() {
      var myHeaders = new Headers();
      
        myHeaders.append("Authorization", "eyJhbGciOiJIUzI1NiJ9.eyJ0aWQiOjE3NzY3Mjg3MCwidWlkIjozMTU0NzE5NiwiaWFkIjoiMjAyMi0wOC0yNlQxNDoyOTo1Ni4wMDBaIiwicGVyIjoibWU6d3JpdGUiLCJhY3RpZCI6MTI1Nzg0NDIsInJnbiI6InVzZTEifQ.dJqhXVLdY1yvpl0x_yADidBgh19NLEZmMiunKQc3N40");
        myHeaders.append("Content-Type", "application/json");
        myHeaders.append("Cookie", "__cf_bm=mwVnwHh171Q7YxRp4Mqj7WoqwBepeDSNJmyT73kNWb8-1661741853-0-Ae1+PHNtWhKRCgi1sXYd2DONKnUkjuEZFpInPBsf0Lu5UoG/AR5rd53TrgnF2e2A4L1AR/P3Kk9825V2oaezod65SZ4VI4oQ8RLOR/n+ziSr");

        var graphql = JSON.stringify({
        query: "mutation myAdd($board_id: Int!,$item_name: String){\n  create_item(board_id: $board_id, item_name: $item_name){\n    id\n    name\n  }\n}",
        variables: {"item_name":"New Item babel","board_id":2845184846}
        })
        var requestOptions = {
        method: 'POST',
        headers: myHeaders,
        body: graphql,
        redirect: 'follow'
        };

        fetch("https://api.monday.com/v2/", requestOptions)
        .then(response => response.text())
        .then(result => console.log(result))
        .catch(error => console.log('error', error));
            },

    }
  };
</script>
<style>
knob-label {
    display: block;
    margin-bottom: 0;
    font-weight: bold;
     color: #febc2c;
}
h1 {
   color: blue;
}
</style>