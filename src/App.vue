<template>
  <div id="app">
    <div>
      <b-button v-b-modal="'modal-1'">Add donation</b-button>
      <b-modal id="modal-1" title="Make A Donation">
        <add-Form></add-Form>
      </b-modal>
    </div>
    <inventory-Table></inventory-Table>
  </div>
</template>

<script>
import Add from "./components/Add.vue";
import Inventory from "./components/Inventory.vue";

export default {
  name: "App",
  components: {
    "add-Form": Add,
    "inventory-Table": Inventory,
  },
  data() {
    return {};
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.center_div {
  margin: 0 auto;
  width: 80%; /* value of your choice which suits your alignment */
}

label {
  font-family: Georgia, "Times New Roman", Times, serif;
  font-size: 18px;
  color: #333;
  height: 20px;
  width: 200px;
  margin-top: 10px;
  margin-left: 10px;
  text-align: right;
  clear: both;
  float: left;
  margin-right: 15px;
}
/* #donationForm {
  display: block;
  padding: 10px 6px;
  width: 35%;
  text-align: center;
  box-sizing: border-box;
  border: none;
  border-bottom: 1px solid #ddd;
  color: #555;
} */
</style>
