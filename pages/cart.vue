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
					value: "item",
				},
				{ text: "ADD ONS", value: "addOns" },
				{ text: "count", value: "count" },
				{ text: "combined price", value: "combinedPrice" },
			],
		};
	},
	computed: {
		carts() {
			return this.$store.state.cart;
		},
	},
};
</script>

<style>
</style>