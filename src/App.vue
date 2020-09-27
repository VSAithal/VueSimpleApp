<template>
  <div id="app" class="container-fluid">
    <Header />
    <div class="list-group">
      <NumberInput
        v-bind:listItems="listItems"
        v-bind:totalValue="totalValue"
        v-on:add-item="addItem"
        v-on:text-change="updateValue"
      />
    </div>
  </div>
</template>

<script>
import NumberInput from "./components/NumberInput";
import Header from "./components/Header";
export default {
  name: "App",
  components: {
    NumberInput,
    Header,
  },
  data() {
    return {
      // Data set containing the initial values
      listItems: [
        {
          id: 1,
          value: 10,
        },
        {
          id: 2,
          value: 20,
        },
        {
          id: 3,
          value: 25,
        },
        {
          id: 4,
          value: 25,
        },
        {
          id: 5,
          value: 20,
        },
      ],
      totalValue: 100,
    };
  },
  methods: {
    // Add new item functionality
    addItem(newItem, addedValue) {
      // Updating the dataset with new added item
      this.listItems = [...this.listItems, newItem];
      // Updating the total value(which displayed on the submit button value)
      this.totalValue = addedValue;
    },
    // updating the values in the dataset and totalValue on change of the text field functionality
    updateValue(id) {
      let totalValue = 0; // Initialising totalValue with 0
      // Updating the dataset with changed value of the text field by copying the updated values with another temporary object variable and returning the same
      const updatedItems = this.listItems.map((item) => {
        let tempList = Object.assign({}, item); // creating a temporary list

        if (id === tempList.id) {
          // checking if the the user leaves the text-field empty
          if (event.target.value === "") {
            // updating value with 0 if left empty
            tempList.value = 0;
            totalValue += 0;
          } else {
            // else taking the value from the text field
            tempList.value = parseInt(event.target.value);
            totalValue += parseInt(event.target.value);
          }
        } else {
          totalValue += tempList.value;
        }
        return tempList;
      });
      this.listItems = {}; // First emptying the state object
      this.listItems = updatedItems; // copying with the updated one
      this.totalValue = totalValue; // updating the total value into the data
    },
  },
};
</script>
<style scoped>
.list-group {
  margin-top: 7%;
}
</style>
