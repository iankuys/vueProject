<template>
  <div id="app">
    <b-container>
      <b-form inline>
        <label>Name:</label>
        <b-form-input
          v-model="product"
          id="inline-form-input-name"
          class="mb-2 mr-sm-2 mb-sm-0"
          placeholder="Jane Doe"
        ></b-form-input>
      </b-form>
    </b-container>

    <b-container>
      <b-form inline>
        <label>Type:</label>
        <b-form-select
          v-model="type"
          :options="options"
          class="mb-2 mr-sm-2 mb-sm-0"
        ></b-form-select>
      </b-form>
    </b-container>

    <b-container>
      <b-form inline>
        <b-form-checkbox
          id="checkbox-1"
          v-model="status"
          name="checkbox-1"
          value="beneficiary"
          class="mb-2 mr-sm-2 mb-sm-0"
        >
          Check if it is beneficiary
        </b-form-checkbox>
      </b-form>
    </b-container>

    <div>
      <button
        type="button"
        @click="handleSubmit"
        class="btn btn-primary mb-2 mr-sm-2 mb-sm-0"
        size="sm"
      >
        Submit
      </button>
    </div>
  </div>
</template>

<script>
import Localbase from "localbase";

let db = new Localbase("db");

export default {
  components: {},
  data() {
    return {
      product: "",
      type: "",
      status: "non-beneficiary",
      options: [
        { value: null, text: "Please select an option" },
        { value: "FoodDonation", text: "Food Donation" },
        { value: "ClothesDonation", text: "Clothes Donation" },
        { value: "2nd Hand Donation", text: "2nd Hand Donation" }
      ],
    };
  },
  methods: {
    handleSubmit() {
      this.addDB();
      this.collectDB();
      this.clearForm();
    },
    addDB() {
      db.collection("donation").add({
        product: this.product,
        type: this.type,
        status: this.status,
      });
    },
    clearForm() {
      this.name = "";
      this.type = "";
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
label {
  display: inline-block;
  width: 140px;
  text-align: right;
}
</style>
