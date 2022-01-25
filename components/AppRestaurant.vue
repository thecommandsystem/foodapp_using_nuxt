<template>
  <v-container>
    <div v-for="store in fooddata" :key="store.id" class="pt-3">
      {{ store.name }}
      <p>Delivery time {{ store.deliveryTime }}</p>
      <p>Rating {{ store.rating }}</p>
      <p v-if="store.freeDelivery" class="label">
        <v-btn color="error"> Free Delivery </v-btn>
      </p>

      <v-row>
        <v-col v-for="menuitem in store.menu" :key="menuitem.id">
          <div>
            <v-card class="mx-auto" max-width="344">
              <v-img :src="menuitem.img" height="200px"></v-img>
              <div>
                <v-card-title> {{ menuitem.item }} </v-card-title>

                <v-card-subtitle> {{ priceFormatting(menuitem.price) }} </v-card-subtitle>
              </div>

              <v-card-actions>
                <nuxt-link :to="`/items/${menuitem.id}`">
                  <v-btn color="orange lighten-2" text> Explore </v-btn>
                </nuxt-link>
                
              </v-card-actions>
            </v-card>
          </div>
        </v-col>
      </v-row>
    </div>
  </v-container>
</template>

<script>
import { mapState } from 'vuex'
export default {
  computed: {
    ...mapState(['fooddata']),
  },

  methods: {
    priceFormatting(item) {
      return '$' + item.toFixed(2)
    },
  },
}
</script>

<style></style>
