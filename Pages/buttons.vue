<template>
  <nb-button :onPress="handleBtnPress">
        <nb-text>Update</nb-text>
      </nb-button>
</template>
<script>
import { ActionSheet } from "native-base";
export default {
  data: function() {
    return {
      btnOptions: [
        { text: "On My Way", icon: "car", iconColor: "#2c8ef4" },
        { text: "Done", icon: "checkmark", iconColor: "#f42ced" },
        { text: "Cancel", icon: "close", iconColor: "#25de5b" }
      ],
      optionCancelIndex: 2,
    
      clicked: 0
    };
  },
  methods: {
    handleBtnPress: function() {
      ActionSheet.show(
        {
          options: this.btnOptions,
          cancelButtonIndex: this.optionCancelIndex,
          destructiveButtonIndex: this.optionDestructiveIndex,
          title: "Select An Option"
        },
        buttonIndex => {
          this.clicked = this.btnOptions[buttonIndex];

        }
      );
    }
  }
};
</script>