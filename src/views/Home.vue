<template>
  <div class="container">
    <Search class="search" />
    <List class="list" />
  </div>
</template>

<script>
import Search from "@/components/Search.vue";
import List from "@/components/List.vue";
export default {
  name: "Home",
  components: {
    Search,
    List
  }
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
