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
        <nb-list-item selected thumbnail @press="alertx(ocu)" v-for="(ocu,key) in ocular_list" :key="key" :on-long-press="() => handleBtnPress(ocu)">
            <nb-body>
              <nb-text>OC#{{ocu.num}}</nb-Text>
              <nb-text note :numberOfLines="2">{{ocu.project_name}}</nb-Text>
            </nb-body>

              <nb-right>
                  <nb-text note>{{ocu.Status}}</nb-text>
                  <nb-text note>{{formattedDate(ocu.schedule)}}</nb-text>
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
import { ActionSheet,Toast } from "native-base";
export default {
  components:{
    Toast
  },
  data() {
    return {
       ocular_list:[],
       client:{},
       query:'',
       searching:false,


      btnOptions: [
        { text: "On My Way", icon: "car", iconColor: "#2c8ef4"  ,action:"On My Way"},
        { text: "Done", icon: "checkmark", iconColor: "#f42ced" ,action:"Done" },
        { text: "Cancel", icon: "close", iconColor: "#25de5b"  }
      ],
      optionCancelIndex: 2,
    
      clicked: 0
    }
  },

  props: {
    navigation: {
      type: Object
    }
  },
  mounted() {
   
    this.getList()
  },
  methods:{
    handleBtnPress: function(x) {
     
      ActionSheet.show(
        {
          options: this.btnOptions,
          cancelButtonIndex: this.optionCancelIndex,
          destructiveButtonIndex: this.optionDestructiveIndex,
          title: "Select Status"
        },
        buttonIndex => {
          this.clicked = this.btnOptions[buttonIndex];
          console.log(this.clicked)
         if (this.clicked.action) {
            
            axios.patch(`http://192.168.1.7:8000/cors/ocularsup/${x.id}`, {
               Status: this.clicked.action
             })
             .then(res => {
                Toast.show({
                  text: "Updating Successfully",
                  buttonText: "Okay",
                  duration:3000,
                   type: "success"
                });
             })
             .catch(err => {
                Toast.show({
                  text: "Updating Failed!",
                  buttonText: "Okay",
                  duration:3000,
                   type: "danger"
                });
             }).then(x=>{
               this.getList()
             })
         }
          
        }
      );
    },
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
          axios.post
      })
    }
  }
}
</script>