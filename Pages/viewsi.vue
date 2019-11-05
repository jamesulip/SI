<template>
  <nb-container class='container'>
    <nb-content v-if="data">

      <nb-card>
        <nb-card-item bordered>
          <nb-body>
            <nb-text class="headtext"><nb-icon class="headtext" :name="'business'" />  Project Name</nb-text>
            <nb-text class="detailstext">Oc# {{data.num.toUpperCase()}}-{{data.project_name.toUpperCase()}}-{{data.clientx.com_name.toUpperCase()}}</nb-text>
          </nb-body>
        </nb-card-item>
        <nb-card-item bordered>
          <nb-body>
            <nb-text class="headtext">Ocular Number</nb-text>
            <nb-text class="detailstext">Oc# {{data.num}}</nb-text>
          </nb-body>
        </nb-card-item>
        <nb-card-item bordered>
          <nb-body>
            <nb-text class="headtext"><nb-icon class="headtext" :name="'people'" /> Client</nb-text>
            <nb-text class="detailstext">{{data.clientx.com_name}}</nb-text>
          </nb-body>
        </nb-card-item>
      </nb-card>
      <nb-card>
        <nb-card-item bordered>
          <nb-body>
            <nb-text class="headtext"><nb-icon class="headtext" :name="'pin'" /> Address</nb-text>
            <nb-text  @press='openurl(data.address)' class="detailstext">{{data.address}}</nb-text>
          </nb-body>
        </nb-card-item>
      </nb-card>
     <nb-card>
        <nb-card-item bordered>
          <nb-body>
            <nb-text class="headtext"><nb-icon class="headtext" :name="'time'" />  Date Requested</nb-text>
            <nb-text class="detailstext">{{data.created_at}}</nb-text>
          </nb-body>
          <nb-body>
            <nb-text class="headtext"><nb-icon class="headtext" :name="'timer'" />   Schedule</nb-text>
            <nb-text class="detailstext">{{data.schedule}}</nb-text>
          </nb-body>
        </nb-card-item>
      </nb-card>

<nb-card>
        <nb-card-item bordered>
          <nb-body>
            <nb-text class="headtext"><nb-icon class="headtext" :name="'contact'" />  Contact Person</nb-text>
            <nb-text class="detailstext">{{data.contact_person}}</nb-text>
          </nb-body>
          <nb-body>
            <nb-text class="headtext"><nb-icon class="headtext" :name="'call'" />   Contact Number</nb-text>
            <nb-text class="detailstext" @press='calltext(data.contact_number)'>{{data.contact_number}}</nb-text>
          </nb-body>
        </nb-card-item>
      </nb-card>
     
      
    </nb-content>
  </nb-container>
</template>

<style>
.headtext{
    font-size:12px
}
.detailstext{
    color:gray;
}
.taable{
    width: 100%;
    font-weight: 700;
}
.rows{
  border-width: 2;
  border-color: #c8e1ff
}
.container {
 
  background-color:#ECF0F5;
}
.heading {
  background-color: darkolivegreen;
}

</style>

<script>
import { Table, Row, Rows } from 'react-native-table-component';
import Vue from 'vue-native-core'
 import {Linking } from 'react-native';
import HTML from 'react-native-render-html'

Vue.component('html', HTML)

export default {
  components:{
     Table, Row, Rows
  },
  props: {
    navigation: {
      type: Object
    }
  },
  data() {
    return {
     
      data: null,
    }
  },
  methods: {
    calltext(num){
        Linking.openURL(`tel:${num}`);
    },
    openurl(url){
     
      Linking.openURL(`https://maps.google.com/?daddr=${url}`).catch(err => console.error("Couldn't load page", err));
    }
  },
  mounted(){
   
    this.data = this.navigation.getParam('data') 
    
  }
}
</script>