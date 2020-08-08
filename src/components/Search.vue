<template>
  <div>
    <select
      type="text"
      placeholder="type"
      v-model="selectedParentSearch"
      @change="ParentSearch()"
    >
      <option v-for="type in fields.Types" :key="type">{{ type }}</option>
    </select>

    <hr />
    <div v-show="selectedParentSearch == 'Advanced Search'">
      <table>
        <tr>
          <td><b>Type</b></td>
          <td>
            <select type="text" v-model="Type">
              <option v-for="type in fields.Advance" :key="type">{{
                type
              }}</option>
            </select>
          </td>
        </tr>

        <tr>
          <td><b>Owner</b></td>
          <td>
            <select type="text" v-model="Owner">
              <option v-for="owner in fields.Owners" :key="owner">{{
                owner
              }}</option>
            </select>
          </td>
        </tr>

        <tr>
          <td><b>Date</b></td>
          <td>
            <select type="text" v-model="selectedDate">
              <option v-for="date in fields.Date" :key="date">{{
                date
              }}</option>
            </select>
          </td>
        </tr>

        <tr v-show="selectedDate == 'Custom...'">
          <td></td>
          <td>
            <input type="date" style="width: 50%;" v-model="startDate" />
            <input type="date" style="width: 50%;" v-model="endDate" />
          </td>
        </tr>

        <tr>
          <td><b>Words</b></td>
          <td>
            <input type="text" class="inputtext" v-model="Title" />
          </td>
        </tr>

        <tr>
          <td><input type="checkbox" v-model="Starred" /> Star</td>
          <td>
            <input type="checkbox" v-model="Trash" />
            In Trash
          </td>
        </tr>
      </table>

      <button @click="submitSearch()">Search</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "Search",
  props: {
    fields: {
      type: Object
    }
  },
  data() {
    return {
      selectedParentSearch: "Advanced Search",
      selectedDate: "",
      Title: "",
      Type: "",
      Owner: "",
      Date: "",
      Starred: "",
      Trash: "",
      startDate: "",
      endDate: (this.Date = new Date()
        .toJSON()
        .slice(0, 10)
        .replace(/-/g, "/"))
    };
  },
  methods: {
    ParentSearch() {
      if (this.selectedParentSearch != "Advanced Search") {
        this.Type = this.selectedParentSearch;
        this.$emit("instantSearch", this.queryString);
      }
    },
    submitSearch() {
      if (this.Owner == "Owned by me") {
        this.Owner = "Khanh";
      } else if (this.Owner == "Anyone") {
        this.Owner = "";
      }

      if (this.Type == "All types") {
        this.Type = "";
      }

      if (this.selectedDate == "Anytime") {
        this.Date = "";
      } else if (this.selectedDate == "Today") {
        this.Date = new Date()
          .toJSON()
          .slice(0, 10)
          .replace(/-/g, "/");
      } else if (this.selectedDate == "Yesterday") {
        this.Date = new Date(new Date().setDate(new Date().getDate() - 1))
          .toJSON()
          .slice(0, 10)
          .replace(/-/g, "/");
      } else {
        if (this.selectedDate == "Last 7 days") {
          this.startDate = this.Date = new Date(
            new Date().setDate(new Date().getDate() - 7)
          )
            .toJSON()
            .slice(0, 10)
            .replace(/-/g, "/");
        }
      }

      console.log(this.queryString);
      console.log(this.startDate);
      console.log(this.endDate);
      this.$emit(
        "DetailSearch",
        this.queryString,
        this.startDate,
        this.endDate
      );
    }
  },
  computed: {
    queryString() {
      return {
        Title: this.Title,
        Type: this.Type,
        Owner: this.Owner,
        Date: this.Date,
        Starred: this.Starred,
        Trash: this.Trash
      };
    }
  }
};
</script>

<style scoped>
select {
  padding: 10px 50px 10px;
  width: 250px;
}

.inputtext {
  width: 243px;
  height: 30px;
}

button {
  margin-top: 10px;
  padding: 13px 20px 13px;
  background-color: orange;
  color: white;
}

td {
  width: 100px;
}
</style>
