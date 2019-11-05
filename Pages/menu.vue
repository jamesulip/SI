<template>
  <nb-container>
    <nb-header searchBar rounded >
      <nb-item>
        <nb-icon active name="search" />
        <nb-input placeholder="Search" v-model="query" :on-end-editing="getList"/>
        <nb-icon active v-if="query" name="close-circle" @press="query=null"/>
      </nb-item>
      <nb-button transparent>
        <nb-text>Search</nb-text>
      </nb-button>
    </nb-header>
    <nb-list>
      <scroll-view>
         
        <nb-list-item itemDivider  v-if="query">
           <nb-text>Search for '{{query}}' result {{ocular_list.length}}</nb-text>
        </nb-list-item>
           <nb-spinner  v-if="searching"/>
        <nb-list-item thumbnail @press="alertx(ocu)" v-for="(ocu,key) in ocular_list" :key="key" >
            <nb-body>
              <nb-text>OC#{{ocu.num}}</nb-Text>
              <nb-text note :numberOfLines="2">{{ocu.project_name}}</nb-Text>
            </nb-body>
              <nb-right>
              <nb-button transparent>
                <nb-icon :name="'timer'"></nb-icon>
                <nb-text>
                    {{formattedDate(ocu.schedule)}}
                </nb-text>
                
              </nb-button>
            </nb-right>
        </nb-list-item>
    </nb-list>
  </nb-container>
</template>
<style>
.headtext{
    font-size:12px
}
.detailstext{
    color:gray;
}
</style>
<script>
import axios from "axios";
import moment from "moment";
export default {
  data() {
    return {
       ocular_list:[],
       client:{},
       query:'',
       searching:false
    }
  },

  props: {
    navigation: {
      type: Object
    }
  },
  methods:{
    formattedDate(x) {
      // alert(x)
        return moment(x,'YYYY-MM-DD hh:mm a').format('MM/DD/YY');
    },
    alertx:function(data){
      this.navigation.navigate("View",{
        data:data
      });
    },
    getList:function(){
      this.searching = true
      axios.get('http://192.168.1.7:8000/cors/oculars?search='+this.query)
      .then(res => {
        // console.log(res)
        this.ocular_list = res.data
        this.searching = false
      })
      .catch(err => {
        console.error(err); 
        alert('asds')
      })
    }
  }
}
</script>