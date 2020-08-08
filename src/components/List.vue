<template>
  <div>
    <ul>
      <li v-for="item in items" :key="item.Title">{{ item }}</li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "List",
  props: {
    items: {
      type: Array,
      required: true,
      default: null
    }
  }
};
</script>

<style scoped>
li {
  text-align: left;
  width: 100%;
}

table {
  width: 100%;
}

tr {
  width: 80%;
}

td {
  width: 200px;
}

ul {
  list-style-type: none;
}
</style>
