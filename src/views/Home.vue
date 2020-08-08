<template>
  <div class="container">
    <Search class="search" />
    <List class="list" :items="items" />
  </div>
</template>

<script>
import Search from "@/components/Search.vue";
import List from "@/components/List.vue";
import EventService from "@/services/EventService.js";

export default {
  name: "Home",
  components: {
    Search,
    List
  },
  data() {
    return {
      fields: null,
      items: []
    };
  },
  created() {
    EventService.getItems()
      .then(respone => {
        this.items = respone.data;
      })
      .catch(error => {
        console.log(error.response);
      });

    EventService.getFields()
      .then(respone => {
        this.fields = respone.data;
      })
      .catch(error => {
        console.log(error.response);
      });
  },
  methods: {}
};
</script>

<style scoped>
.search {
  width: 30%;
  height: 100%;
  position: relative;
  border-right: 1px solid gray;
}

.list {
  width: 70%;
  height: 100%;
  position: relative;
}

.container {
  width: 100%;
  height: 100%;
  position: absolute;
  display: flex;
}
</style>
