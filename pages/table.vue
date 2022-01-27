<template>
	<v-row no-gutters class="pa-4">
		<v-col cols="12">
			<v-btn small @click="set_person(default_person, true, 'create')">
				create person
			</v-btn>
		</v-col>
		<v-col cols="12" class="mt-4">
			<v-card outlined width="100%">
				<v-data-table :headers="headers" :items="people" height="60vh">
				</v-data-table>
			</v-card>
		</v-col>

		<v-dialog v-model="dialog" max-width="400px" persistent>
			<v-card>
				<v-form v-model="valid" @submit.prevent="create_person(person)">
					<v-row no-gutters class="pa-4">
						<v-col cols="12">
							<v-text-field
								v-model="person.firstname"
								label="Firstname"
								dense
								outline
							></v-text-field>
						</v-col>

						<v-col cols="12" class="mt-3">
							<v-text-field
								v-model="person.middlename"
								label="Middlename"
								dense
								outline
							></v-text-field>
						</v-col>

						<v-col cols="12" class="mt-3">
							<v-text-field
								v-model="person.lastname"
								label="Lastname"
								dense
								outline
							></v-text-field>
						</v-col>

						<v-col cols="12" class="mt-3">
							<v-text-field
								v-model="person.age"
								label="Age"
								type="number"
								dense
								outline
							></v-text-field>
						</v-col>

						<v-col cols="12" class="mt-4">
							<v-row no-gutters>
								<v-col cols="12" lg="6" class="pa-2">
									<v-btn block @click="set_person(default_person, false)">
										cancel
									</v-btn>
								</v-col>

								<v-col cols="12" lg="6" class="pa-2">
									<v-btn block type="submit" :disabled="!valid"> submit </v-btn>
								</v-col>
							</v-row>
						</v-col>
					</v-row>
				</v-form>
			</v-card>
		</v-dialog>
	</v-row>
</template>

<script>
export default {
	data() {
		return {
			headers: [
				{
					text: "Firstname",
					value: "firstname",
					align: "center",
					class: "text-uppercase font-weight-bold",
				},
				{
					text: "Middlename",
					value: "middlename",
					align: "center",
					class: "text-uppercase font-weight-bold",
				},
				{
					text: "Lastname",
					value: "lastname",
					align: "center",
					class: "text-uppercase font-weight-bold",
				},
				{
					text: "Age",
					value: "age",
					align: "center",
					class: "text-uppercase font-weight-bold",
				},
			],
			people: [],
			person: {
				firstname: null,
				middlename: null,
				lastname: null,
				age: 0,
			},
			default_person: {
				firstname: null,
				middlename: null,
				lastname: null,
				age: 0,
			},
			dialog: false,
			mode: null,
			valid: false,
		};
	},

	computed: {
		formatted_people() {
			return this.people && this.people.length
				? this.people.map((person) => {
						return {
							...person,
							name: `${person.firstname} ${person.middlename || ""} ${
								person.lastname
							}`,
						};
				  })
				: [];
		},
	},

	methods: {
		set_person(person, dialog, mode) {
			this.person = { ...person };
			this.dialog = dialog;
			this.mode = mode;
		},
		create_person(person) {
			this.people.push(person);
			this.set_person(this.default_person);
		},
	},
};
</script>

<style>
</style>