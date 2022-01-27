<template>
<v-container>
   
    <v-data-table
      dense
      :headers="headers"
      :items="carts"
      item-key="name"
      class="elevation-1"
    ></v-data-table>

</v-container>
 
</template>

<script>


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
      carts: []
    };
  },
  computed: {
    cart() {
      return this.carts = this.$store.state.cart;
    },
  },
};
</script>

<style>
</style>