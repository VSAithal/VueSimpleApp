<template>
  <div>
    <form @submit="addTodo">
      <div class="input-group">
        <input
          type="text"
          class="form-control"
          name="title"
          v-model="title"
          placeholder="Type in the Todo title here..    "
        />
        <div class="input-group-btn">
          <!-- <button class="btn btn-primary defButton" type="submit" >
            Add New
          </button> -->
          <input
            type="submit"
            value="Submit"
            class="btn btn-primary defButton"
          />
        </div>
      </div>
    </form>
  </div>
</template>
<script>
// import { v4 as uuidv4 } from "uuid";
export default {
  name: "AddTodos",
  data() {
    return {
      title: "",
    };
  },
  methods: {
    addTodo(e) {
      e.preventDefault();
      const newTodo = {
        // id: uuidv4(),
        title: this.title,
        completed: false,
      };
      this.$emit("add-todo", newTodo);
      this.title = "";
    },
  },
};
</script>
<style scoped></style>
