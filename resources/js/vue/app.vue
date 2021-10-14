<template>
  <div class="todoListContainer">
    <div class="heading">
      <h2 id="title">Todo List</h2>
      <add-item 
        v-on:reloadlist="getList()"
       />
    </div>

    <list-view :items="items"
    v-on:reloadlist="getList()"/>
  </div>
</template>

<script>
import addItem from "./addItem";
import ListView from "./listView.vue";

export default {
  components: {
    addItem,
    ListView,
  },
  data: function () {
    return {
      items: [],
    };
  },
  methods: {
    getList() {
      axios
        .get("api/items")
        .then((response) => {
          this.items = response.data;
        })
        .catch((error) => {
          console.log(error);
        });
    },
  },
  created() {
      this.getList();
  },
};
</script>

<style scoped>
.todoListContainer {
  width: 350px;
  margin: auto;
}

.heading {
  padding: 10px;
  background-color: #e6e6e6;
}

#title {
  text-align: center;
}
</style>