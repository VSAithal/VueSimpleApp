<template>
  <div>
    <form @submit="addItem">
      <div v-for="item in listItems" v-bind:key="item.id">
        <ListItem
          v-bind:item="item"
          v-on:text-change="$emit('text-change', item.id)"
        />
      </div>
      <input type="submit" class="inputStyle" :value="totalValue" />
    </form>
  </div>
</template>
<script>
import ListItem from "./ListItem";
import { v4 as uuidv4 } from "uuid"; // id generator
export default {
  name: "NumberInput",
  props: ["listItems", "totalValue"],
  components: { ListItem },
  methods: {
    addItem(e) {
      e.preventDefault(); // preventing from the form getting submitted
      const newVal = Math.floor(Math.random() * 11); // generating a random integer from 0 to 10 and assigning it to a variable
      // creating new object with new values
      const newItem = {
        id: uuidv4(),
        value: newVal,
      };
      const addedValue = this.totalValue + newVal; // updating the total value
      this.$emit("add-item", newItem, addedValue);
    },
  },
};
</script>
<style scoped>
input[type="submit"] {
  margin-top: 1%;
  background: #3e3d3d !important;
}
</style>
