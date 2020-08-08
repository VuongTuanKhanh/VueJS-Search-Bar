<template>
  <div class="contact-box">
    <div class="container">
      <div class="row">
        <div class="col-lg-12">
          <div class="heading-title text-center">
            <h2>{{ title }}</h2>
            <p>
              Generate a new page or a new site
            </p>
          </div>
        </div>
      </div>
      <div class="row">
        <div class="col-lg-12">
          <form
            id="contactForm"
            novalidate="true"
            @submit.prevent="AddNewItem()"
          >
            <div class="row">
              <div class="col-md-12">
                <div class="form-group">
                  <input
                    type="text"
                    class="form-control"
                    placeholder="Item Name"
                    v-model="name"
                  />
                </div>
              </div>
              <div class="col-md-12">
                <div class="form-group">
                  <input
                    type="text"
                    class="form-control"
                    placeholder="Owner"
                    v-model="owner"
                  />
                </div>
              </div>

              <div class="col-md-12">
                <div class="form-group">
                  <input type="date" class="form-control" v-model="date" />
                </div>
              </div>

              <div class="col-md-12">
                <div class="form-group">
                  <input type="checkbox" v-model="starred" /> Star

                  <input
                    type="checkbox"
                    placeholder="Owner"
                    name="name"
                    style="margin-left: 200px"
                    v-model="trash"
                  />
                  In Trash
                </div>
              </div>

              <div style="width: 100%">
                <select type="text" v-model="type">
                  <option v-for="type in types" :key="type">{{ type }}</option>
                </select>
              </div>

              <div class="col-md-12">
                <div class="submit-button text-center">
                  <button
                    class="btn btn-common disabled"
                    id="submit"
                    type="submit"
                    style="pointer-events: all; cursor: pointer;"
                  >
                    {{ btn_text }}
                  </button>
                  <div id="msgSubmit" class="h3 text-center hidden"></div>
                  <div class="clearfix"></div>
                </div>
              </div>
            </div>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Form",
  props: {
    fields: {
      type: Object
    },
    title: {
      type: String,
      default: "Create new Item"
    },
    btn_text: {
      type: String,
      default: "Add Item"
    }
  },
  data() {
    return {
      name: "",
      owner: "",
      date: "",
      starred: false,
      trash: false,
      type: "Sites",
      types: ["Sites", "Pages"],
      owners: ["Anyone", "Owned by me", "Not owned by me"]
    };
  },
  methods: {
    AddNewItem() {
      let Item = {
        Title: this.name,
        Type: this.type,
        Owner: this.owner,
        Date: this.date,
        Starred: this.starred,
        Trash: this.trash
      };
      console.log("Add", Item);
      this.$emit("SendItem", Item);
      this.name = null;
      this.owner = null;
      this.date = null;
      this.starred = false;
      this.trash = false;
      this.type = "Sites";
    }
  }
};
</script>

<style scoped>
select {
  width: 100%;
  padding: 0.375rem 0.75rem;
  font-size: 1rem;
  line-height: 1.5;
  color: #495057;
  background-color: #fff;
  background-clip: padding-box;
  border: 1px solid #ced4da;
  border-radius: 0.25rem;
  transition: border-color 0.15s ease-in-out, box-shadow 0.15s ease-in-out;
  margin-right: 20px;
  margin-left: 20px;
}

.container {
  height: 100%;
  width: 100%;
  position: relative;
  overflow: hidden;
  text-align: center;
}
.contact-box {
  padding: 70px 0px;
}
.row {
  display: flex;
  flex-wrap: wrap;
  margin-right: 15px;
  margin-left: 15px;
}
.col-lg-12 {
  position: relative;
  width: 100%;
  min-height: 1px;
  padding-right: 15px;
  padding-left: 15px;
}
.heading-title {
  margin-bottom: 50px;
}

.text-center {
  text-align: center !important;
}
.heading-title h2 {
  color: #010101;
  font-size: 28px;
  font-family: "Rubik", sans-serif;
  font-weight: 500;
  letter-spacing: 0;
  font-weight: normal;
  position: relative;
  padding: 0 0 10px 0;
  font-weight: normal;
  line-height: 120% !important;
  color: #1f1f1f;
  margin: 0;
}
.col-md-12 {
  position: relative;
  width: 100%;
  min-height: 1px;
  padding-right: 15px;
  padding-left: 15px;
  margin-bottom: 20px;
}

.btn.btn-common {
  color: white;
  background-color: transparent;
  background-image: none;
  background-color: #d65106;
  margin-top: 20px;
  padding: 15px 25px 15px;
}

.form-control {
  border-radius: 0px;
  min-height: 50px;
}
.form-control {
  display: block;
  width: 100%;
  padding: 0.375rem 0.75rem;
  font-size: 1rem;
  line-height: 1.5;
  color: #495057;
  background-color: #fff;
  background-clip: padding-box;
  border: 1px solid #ced4da;
  border-radius: 0.25rem;
  transition: border-color 0.15s ease-in-out, box-shadow 0.15s ease-in-out;
}
input {
  margin: 0;
  font-family: inherit;
  font-size: inherit;
  line-height: inherit;
}
select.form-control:not([size]):not([multiple]) {
  height: calc(2.25rem + 2px);
}
option {
  font-weight: normal;
  display: block;
  white-space: pre;
  min-height: 1.2em;
  padding: 0px 2px 1px;
}
</style>
