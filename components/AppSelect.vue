<template>
  <div>
    <v-data-iterator>
      <template v-slot:header>
        <v-toolbar dark color="blue darken-3" class="mb-1">
          <v-text-field
            :v-model="select"
            clearable
            flat
            solo-inverted
            hide-details
            prepend-inner-icon="mdi-magnify"
            label="Search"
          ></v-text-field>
          <template v-if="$vuetify.breakpoint.mdAndUp">
            <v-spacer></v-spacer>
            <v-select
              @input="changeSelect()"
              :placeholder="select"
              v-model="selectValue"
              flat
              solo-inverted
              hide-details
              :items="selectOptions"
              prepend-inner-icon="mdi-magnify"
              label="Please select a cuisine"
            ></v-select>
            <v-spacer></v-spacer>
            <v-btn-toggle mandatory>
              <v-btn large depressed color="blue" :value="false">
                <v-icon>mdi-arrow-up</v-icon>
              </v-btn>
              <v-btn large depressed color="blue" :value="true">
                <v-icon>mdi-arrow-down</v-icon>
              </v-btn>
            </v-btn-toggle>
          </template>
        </v-toolbar>
      </template>
    </v-data-iterator>

  </div>
</template>

<script>
// https://stackoverflow.com/questions/58430391/how-to-use-v-model-and-props-passed-to-parent-from-child
export default {
  data() {
    return {
      selectValue: '',
    }
  },
  watch: {},
  props: {
    select: {
      type: String,
      default: 'restaurant',
    },
    selectOptions: {
      type: Array,
      default: () => ['tacos', 'pizza', 'dim sum'],
    },
  },
  methods: {
    changeSelect() {
      this.$emit('input', this.selectValue)
    },
  },
}
</script>

<style></style>
