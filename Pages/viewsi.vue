<template>
  <nb-container>
    <view class="container">
      <text class="heading">{{data.com_name}}</text>
      <text class="text">This is the Home screen</text>
      <text class="text">Use the swipe gesture to open the drawer navigator</text>
    </view>
  </nb-container>
</template>

<style>
.container {
  align-items: center;

  flex: 1;
  padding: 50px;
  padding-top:5px;
}
.heading {
  font-size: 30px;
  font-weight: bold;
  color: darkolivegreen;
  margin: 20px;
}
.text {
  text-align: center;
  margin: 10px;
}
</style>

<script>
export default {
  props: {
    navigation: {
      type: Object
    }
  },
  data() {
    return {
      data:{
        "ID": "5d0c5337abd0d",
        "com_address": null,
        "com_cathegory": null,
        "com_industry": "123",
        "com_name": "Tigergraphics",
        "com_products": "123",
        "com_vat": "Company",
        "companycol": null,
        "created_at": "2019-07-26 14:58:40",
        "deleted_at": null,
        "notes": null,
        "salesExec": "WzSdAX57iu",
        "updated_at": "2019-07-26 14:58:40",
      },
    }
  },
  mounted(){
    //  console.log(this.navigation.getParam('data'))
  }
}
</script>