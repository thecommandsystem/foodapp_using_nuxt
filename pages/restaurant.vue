<template>
  <v-container>
    <div>
      <h1>Restaurant</h1>
      <AppSelect :placeholder="selectedRestaurant" v-model="selectedRestaurant" />
   
    </div>
    <AppRestaurant :datasource="filterRestaurant" />
  </v-container>
</template>

<script>
import {mapState} from 'vuex'
export default {
  data() {
    return {
      selectedRestaurant: '',
    }
  },
  computed: {
    ...mapState(["fooddata"]),
    filterRestaurant() {
      if (this.selectedRestaurant) {
        return this.fooddata.filter((el) => {
          let name = el.name.toLowerCase();
          return name.includes(this.selectedRestaurant)
        })
      }
      return this.fooddata;
    }
  },
  methods: {},
}
</script>

<style></style>
