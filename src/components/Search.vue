<template>
  <div>
    <select
      type="text"
      placeholder="type"
      @change="onTypeChange()"
      v-model="selectedSearch"
    >
      <option v-for="type in fields.Types" :key="type">{{ type }}</option>
    </select>

    <hr />
    <div v-show="selectedSearch == 'Advanced Search'">
      <table>
        <tr>
          <td><b>Type</b></td>
          <td>
            <select type="text">
              <option v-for="type in fields.Advance" :key="type">{{
                type
              }}</option>
            </select>
          </td>
        </tr>

        <tr>
          <td><b>Owner</b></td>
          <td>
            <select type="text">
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
            <input type="date" style="width: 50%;" />
            <input type="date" style="width: 50%;" />
          </td>
        </tr>

        <tr>
          <td><b>Words</b></td>
          <td>
            <input type="text" class="inputtext" />
          </td>
        </tr>

        <tr>
          <td><input type="checkbox" v-model="isStarred" /> Star</td>
          <td>
            <input type="checkbox" v-model="isTrash" />
            In Trash
          </td>
        </tr>
      </table>

      <button>Search</button>
    </div>
  </div>
</template>

<script>
import EventService from "@/services/EventService.js";
export default {
  name: "Search",
  data() {
    return {
      fields: {
        Types: null,
        Owners: null,
        Persons: null,
        Starred: null,
        Trash: null,
        Date: null
      },
      selectedSearch: "Advanced Search",
      selectedDate: "Anytime",
      isStarred: false,
      isTrash: false,
      queryString: ""
    };
  },
  methods: {
    onTypeChange() {
      this.$emit("SendQuery", "Pages");
    }
  },
  created() {
    EventService.getFields()
      .then(respone => {
        this.fields = respone.data;
      })
      .catch(error => {
        console.log(error.response);
      });
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
