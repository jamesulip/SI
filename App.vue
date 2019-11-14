<template>
  <root>
    <app-navigator title="Skrrrrt" v-if="isAppReady"></app-navigator>
    <AppLoading v-else/>
  </root>
</template>

<script>
import { Root,VueNativeBase,Toast  } from "native-base";
import {
  createAppContainer,
  createStackNavigator,
  createDrawerNavigator
} from "vue-native-router";
import { AppLoading } from 'expo';
import HomeScreen from "./Pages/menu.vue";
import View from "./Pages/viewsi.vue";


const DrawerNavigator = createDrawerNavigator(
  {
    
    Home: HomeScreen,
    View:View 
  },
  {
    initialRouteName: 'Home'
  }
);

const StackNavigator = createStackNavigator({
  Drawer: DrawerNavigator,
  Home: HomeScreen,
  View:View
}, 
{
  initialRouteName: 'Home',
});

const AppNavigator = createAppContainer(StackNavigator);
import Vue from "vue-native-core";
import * as Font from 'expo-font';
import {  Ionicons } from '@expo/vector-icons';
Vue.use(VueNativeBase);


export default {
  components: {
    AppNavigator,
    AppLoading,
    Root,
    Toast 
  },
  data() {
    return {
      isAppReady:false
    }
  },
  mounted() {
    this.loadFonts()
  },
  methods: {
    loadFonts: async function () {
      try {
        this.isAppReady = false;
        await Expo.Font.loadAsync({
          Roboto: require("native-base/Fonts/Roboto.ttf"),
          Roboto_medium: require("native-base/Fonts/Roboto_medium.ttf"),
          ...Ionicons.font,
        });
        this.isAppReady = true;
      } catch (error) {
        console.log("some error occured", error);
        this.isAppReady = true;
      }
    }

  },
}
</script>