<template>
  <v-container>
    <div>
      <h1>Restaurant</h1>
      <AppSelect :placeholder="selectedRestaurant" v-model="selectedRestaurant" />
      <pre>{{ $data }}</pre>
    </div>
    <AppRestaurant />
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      selectedRestaurant: '',
    }
  },
  methods: {},
}
</script>

<style></style>
