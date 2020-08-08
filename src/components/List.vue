<template>
  <div>
    <ul>
      <li v-for="item in showList" :key="item.Title">{{ item }}</li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "List",
  props: {
    items: {
      type: Array
    },
    query: {
      type: Object
    }
  },
  data() {
    return {
      showList: []
    };
  },
  watch: {
    items() {
      this.showList = this.items;
    },
    query() {
      this.showList = [];
      let query_Attr = Object.values(this.query);
      for (let i of this.items) {
        let item_Attr = Object.values(i);
        for (let j in item_Attr) {
          if (item_Attr[j] != query_Attr[j] && query_Attr[j] != "") {
            this.showList.push(i);
            break;
          }
        }
      }
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
