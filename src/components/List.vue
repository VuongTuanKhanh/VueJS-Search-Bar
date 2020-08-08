<template>
  <div>
    <table border="1">
      <tr>
        <td></td>
        <td><h3>Title</h3></td>
        <td><h3>Type</h3></td>
        <td><h3>Owner</h3></td>
        <td><h3>Date</h3></td>
        <td><h3>Starred</h3></td>
        <td><h3>Trash</h3></td>
      </tr>
      <tr v-for="(item, index) in showList" :key="item.Title">
        <td>{{ index }}</td>
        <td>{{ item.Title }}</td>
        <td>{{ item.Type }}</td>
        <td>{{ item.Owner }}</td>
        <td>{{ item.Date }}</td>
        <td>{{ item.Starred }}</td>
        <td>{{ item.Trash }}</td>
      </tr>
    </table>
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
    },
    advanceQuery: {
      type: Object
    },
    startDate: {
      type: String
    },
    endDate: {
      type: String
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
          if (item_Attr[j] == query_Attr[j] && query_Attr[j] != "") {
            this.showList.push(i);
            break;
          }
        }
      }
    },
    advanceQuery() {
      this.showList = [];
      // eslint-disable-next-line no-unused-vars
      let start = new Date(this.startDate);
      // eslint-disable-next-line no-unused-vars
      let end = new Date(this.endDate);
      console.log("Advance Query", this.advanceQuery);
      for (let item of this.items) {
        if (
          item["Type"] != this.advanceQuery["Type"] &&
          this.advanceQuery["Type"] != ""
        ) {
          continue;
        }

        if (this.advanceQuery["Owner"] == "Not owned by me") {
          if (item["Owner"] == "Khanh") {
            continue;
          }
        } else if (
          item["Owner"] != this.advanceQuery["Owner"] &&
          this.advanceQuery["Owner"] != ""
        ) {
          continue;
        }

        if (
          item["Starred"] != this.advanceQuery["Starred"] &&
          this.advanceQuery["Starred"] != ""
        ) {
          continue;
        }

        if (
          item["Trash"] != this.advanceQuery["Trash"] &&
          this.advanceQuery["Trash"] != ""
        ) {
          continue;
        }

        if (
          this.advanceQuery["Title"] != "" &&
          item["Title"]
            .toUpperCase()
            .includes(this.advanceQuery["Title"].toUpperCase()) == false
        ) {
          continue;
        }

        if (this.advanceQuery["Date"] != "") {
          if (item["Date"] != this.advanceQuery["Date"]) continue;
        } else if (this.advanceQuery["Date"] == "") {
          let current = new Date(item.Date);
          if (start <= current && current <= end) {
            this.showList.push(item);
            continue;
          }
        }
        this.showList.push(item);
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
  width: 90%;
  margin: auto;
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
