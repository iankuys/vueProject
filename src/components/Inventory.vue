<template>
  <div>
    <h3>Inventory</h3>
    <table class="table table-white">
      <thead>
        <tr>
          <th scope="col">#</th>
          <th scope="col">ProductName</th>
          <th scope="col">Type</th>
          <th scope="col">Status</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(entry, i) in allInventory" :key="i">
          <th scope="row">{{ ++i }}</th>
          <td>{{ entry.product }}</td>
          <td>{{ entry.type }}</td>
          <td>{{ entry.status }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import Localbase from "localbase";

let db = new Localbase("db");

export default {
  data() {
    return {
      allInventory: [],
    };
  },
  created() {
    this.collectDB();
  },
  methods: {
    collectDB() {
      db.collection("donation")
        .get()
        .then((donation) => {
          console.log(donation);
          this.allInventory = donation;
        });
      this.$forceUpdate();
    },
  },
};
</script>
