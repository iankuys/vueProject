<template>
  <div>
    <h3>Inventory</h3>
    <button
      type="button"
      @click="refreshInventory"
      class="btn btn-primary mb-2 mr-sm-2 mb-sm-0"
      size="sm"
    >
      Refresh
    </button>
    <button
      type="button"
      @click="filterByBeneficiary"
      class="btn btn-primary mb-2 mr-sm-2 mb-sm-0"
      size="sm"
    >
      Filter By Status
    </button>
    <table class="table table-white">
      <thead>
        <tr>
          <th scope="col">#</th>
          <th scope="col">ProductName</th>
          <th scope="col">Type</th>
          <th scope="col">Status</th>
        </tr>
      </thead>
      <template v-if="isBeneficiary === false">
        <tbody>
          <tr v-for="(entry, i) in allInventory" :key="i">
            <th scope="row">{{ ++i }}</th>
            <td>{{ entry.product }}</td>
            <td>{{ entry.type }}</td>
            <td>{{ entry.status }}</td>
          </tr>
        </tbody>
      </template>
      <template v-else>
        <tbody>
          <tr v-for="(entry, i) in benficiaryInventory" :key="i">
            <th scope="row">{{ ++i }}</th>
            <td>{{ entry.product }}</td>
            <td>{{ entry.type }}</td>
            <td>{{ entry.status }}</td>
          </tr>
        </tbody>
      </template>
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
      benficiaryInventory: [],
      isBeneficiary: false,
    };
  },
  created() {
    this.collectDB();
  },
  methods: {
    filterByBeneficiary() {
      this.isBeneficiary = true;
      this.collectBeneficiaryDB();
    },
    collectDB() {
      db.collection("donation")
        .get()
        .then((donation) => {
          console.log(donation);
          this.allInventory = donation;
        });
    },
    refreshInventory() {
      window.location.reload();
    },
    collectBeneficiaryDB() {
      this.benficiaryInventory = this.allInventory.filter(function (el) {
        return el.status == "beneficiary";
      });
      // this.allInventory.forEach((element, array) => {
      //   if (element.status == "beneficiary") {
      //     console.log(array);
      //     this.benficiaryInventory = array;
      //   }
      // });
    },
  },
};
</script>
