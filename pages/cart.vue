<template>
<v-container>
   <div v-for="item in cart" :key="item.id">
    <v-data-table
      dense
      :headers="headers"
      :items="item.item"
      item-key="name"
      class="elevation-1"
    ></v-data-table>
  </div>
</v-container>
 
</template>

<script>
import { mapState } from "vuex";

export default {
  data() {
    return {
      headers: [
        {
          text: "Item",
          align: "start",
          sortable: false,
          value: "name",
        },
        { text: "ADD ONS", value: "calories" },
        { text: "Amount", value: "fat" },
        { text: "Total Price", value: "carbs" },
      
      ],
    };
  },
  computed: {
    cart() {
      return this.$store.state.cart;
    },
  },
};
</script>

<style>
</style>