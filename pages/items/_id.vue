<template>
  <div class="pa-5">
    <v-row no-gutters>
      <v-col cols="4">
        <v-card class="pa-2" outlined tile>
          <v-img :src="currentItem.img" height="500px" :eager="true"></v-img>
        </v-card>
      </v-col>
      <v-col cols="6">
        <div class="pl-2">
          <div>
            <h1>{{ currentItem.item }}</h1>
          </div>

          <h3>Price: ${{ currentItem.price.toFixed(2) }}</h3>
        </div>
        <div class="pa-2">
          <v-row>
            <v-col>
              <v-text-field label="1" solo v-model="count"></v-text-field>
            </v-col>
            <v-col>
              <v-btn depressed color="primary" @click="addtoCart">
                Add to cart - ${{ combinedPrice }}
              </v-btn>
            </v-col>
          </v-row>
        </div>
        <div v-if="currentItem.options" class="pa-2">
          <v-card class="pa-2">
            <v-card-title> options </v-card-title>
            <div
              v-for="option in currentItem.addOns"
              :key="option"
              class="pa-2"
            >
              <v-checkbox
                v-model="itemOptions"
                :label="option"
                color="red"
                :value="option"
                hide-details
              ></v-checkbox>
            </div>
          </v-card>
        </div>

        <div v-if="currentItem.addOns" class="pa-2">
          <v-card>
            <v-card-title> Addons </v-card-title>
            <div v-for="option in currentItem.addOns" :key="option">
              <v-checkbox
                class="pa-2"
                v-model="itemAddons"
                :label="option"
                color="red"
                :value="option"
                hide-details
              ></v-checkbox>
            </div>
          </v-card>
        </div>
      </v-col>
      <v-col>
        <v-card v-if="cartSubmitted">
          <div class="pa-2">
            <AppToast
              >Order Submited <br />
              Check out more <nuxt-link to="/restaurant">Restaurant</nuxt-link>
            </AppToast>
          </div>
        </v-card>
      </v-col>
    </v-row>

    <div class="pa-2">
      <h3>Description</h3>
      <p>{{ currentItem.description }}</p>
    </div>
  </div>
</template>

<script>
import { mapState } from "vuex";
export default {
  data() {
    return {
      id: this.$route.params.id,
      count: 1,
      itemOptions: "",
      itemAddons: [],
      itemSizeAndCost: [],
      cartSubmitted: false,
    };
  },
  computed: {
    ...mapState(["fooddata"]),
    currentItem() {
      let result;
      for (let i = 0; i < this.fooddata.length; i++) {
        for (let j = 0; j < this.fooddata[i].menu.length; j++) {
          if (this.fooddata[i].menu[j].id === this.id) {
            result = this.fooddata[i].menu[j];
            break;
          }
        }
      }

      return result;
    },
    combinedPrice() {
      let total = this.count * this.currentItem.price;
      return total.toFixed(2);
    },
  },
  methods: {
    addtoCart() {
      let formOutput = {
        item: this.currentItem.item,
        count: this.count,
        options: this.itemOptions,
        addOns: this.itemAddons,
        combinedPrice: this.combinedPrice,
      };

      this.cartSubmitted = true;
      this.$store.commit("addToCart", formOutput);
    },
  },
};
</script>

<style>
</style>