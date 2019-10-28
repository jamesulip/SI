<template>
  <nb-container>
    <nb-content>
      <nb-card>
        <nb-card-item header>
          <nb-text>{{data.com_name}}</nb-text>
        </nb-card-item>
        <nb-card-item bordered>
          <nb-body>
            <nb-text>TIN:</nb-text>
            <nb-text>{{data.tin}}</nb-text>
          </nb-body>
        </nb-card-item>
        <nb-card-item bordered>
          <nb-body>
            <nb-text>Address:</nb-text>
            <nb-text>{{data.com_address}}</nb-text>
          </nb-body>
        </nb-card-item >
      </nb-card>

      <nb-card-item bordered>
        <nb-body>
          <table>
            <row :data="tableHead" />
            <rows :data="tableData" class="rows"/>
          </table>
        </nb-body>
      </nb-card-item>
    </nb-content>
  </nb-container>
</template>

<style>
.rows{
  border-width: 2;
  border-color: #c8e1ff
}
.container {
  align-items: center;

  flex: 1;
  padding: 50px;
  padding-top:5px;
}
.heading {
  font-size: 15px;
  font-weight: bold;
  color: darkolivegreen;
  margin: 10;
}
.text {
  text-align: center;
  margin: 10px;
}
</style>

<script>
import { Table, Row, Rows } from 'react-native-table-component';
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
      tableHead: ['Head', 'Head2', 'Head3', 'Head4'],
      tableData: [
        ['1', '2', '3', '4'],
        ['a', 'b', 'c', 'd'],
        ['1', '2', '3', '456\n789'],
        ['a', 'b', 'c', 'd']
      ],
      data:{
        "ID": "5d0c5337abd0d",
        "com_address": 'Cecilia Chapman711-2880 Nulla St.Mankato Mississippi 96522(257) 563-7401',
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
        'tin':'006-329-380-000'
      },
    }
  },
  mounted(){
    this.data = this.navigation.getParam('data') || this.data
    //  console.log(this.navigation.getParam('data'))
  }
}
</script>