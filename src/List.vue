<template>
  <table class="table">
    <thead>
      <tr>
        <th>#</th>
        <th>UserID</th>
        <th>Title</th>
      </tr>
    </thead>
    <tbody>
      
      <listItem 
        v-for="item in items"
        :item="item"
        :key="item.id"
        @viewDetails="viewDetails"
      ></listItem>
    </tbody>
  </table>
</template>

<script>
import ListItem from "./ListItem.vue";
import _ from "lodash";

export default {
  components: {
    ListItem
  },
  data() {
    return {
      items: []
    }
  },
  created() {
    this.fetchData();
  },
  methods: {
    fetchData() {
      this.$http.get("https://jsonplaceholder.typicode.com/posts")
        .then(result => {
           this.items = result.data
      });
    },
    viewDetails(id) {
      let itemToView = _.find(this.items, { id: id });
      this.$emit("viewDetails", itemToView);
    }
  }
}
</script>

<style>
</style>
