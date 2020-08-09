<template>
  <div>
    <Create @SendItem="AddItemToList" />
    <div class="container">
      <Search
        class="search"
        :fields="fields"
        @instantSearch="ExecuteInstantSearch"
        @AdvanceSearch="ExecuteAdvanceSearch"
      />
      <List
        class="list"
        :items="items"
        :query="query"
        :advanceQuery="advanceQuery"
        :startDate="startDate"
        :endDate="endDate"
        @Finish="ClearData"
      />
    </div>
  </div>
</template>

<script>
import EventService from "@/services/EventService.js";
import Search from "@/components/Search.vue";
import List from "@/components/List.vue";
import Create from "@/components/Create.vue";

export default {
  name: "Home",
  components: {
    Search,
    List,
    Create
  },
  data() {
    return {
      fields: {
        Owners: null,
        Types: null
      },
      items: [],
      query: {
        Title: "",
        Type: "",
        Owner: "",
        Date: "",
        Starred: "",
        Trash: ""
      },
      advanceQuery: {
        Title: "",
        Type: "",
        Owner: "",
        Date: "",
        Starred: "",
        Trash: ""
      },
      startDate: "",
      endDate: ""
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
  methods: {
    AddItemToList(newItem) {
      this.items.push(newItem);
    },
    ExecuteInstantSearch(newQuery) {
      this.query = newQuery;
    },
    ExecuteAdvanceSearch(newQuery, startDate, endDate) {
      this.advanceQuery = newQuery;
      this.startDate = startDate;
      this.endDate = endDate;
    },
    ClearData() {
      this.startDate = "";
      this.endDate = "";
    }
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
  height: 50%;
  position: absolute;
  display: flex;
}

.container1 {
  width: 100%;
  height: 50%;
  position: absolute;
}
</style>
