<script>
import AppHeader from "./components/AppHeader.vue";
import AppMain from "./components/AppMain.vue";
import store from "./data/store.js";
import axios from "axios";

export default {
	name: "App",
	components: {
		AppHeader,
		AppMain,
		store,
	},
	data() {
		return {
			cardUrl: "https://db.ygoprodeck.com/api/v7/cardinfo.php?num=200&offset=0",
			archetypeUrl: "https://db.ygoprodeck.com/api/v7/archetypes.php",
			selected: "",
			store,
		};
	},
	created() {
		axios.get(this.cardUrl).then((result) => {
			this.store.cards = result.data.data;
		});

		axios.get(this.archetypeUrl).then((result) => {
			this.store.archetypeList = result.data;
		});
	},
};
</script>

<template>
	<AppHeader />
	<div class="mainBox py-4">
		<select class="form-select mb-4" v-model="selected">
			<option selected value="">Select the archetype</option>
			<option v-for="archetype in store.archetypeList">{{ archetype.archetype_name }}</option>
		</select>

		<AppMain />
	</div>
</template>

<style scoped>
.mainBox {
	background-color: #d48f38;
	padding: 0 12rem;
}

select {
	margin-left: 3.5rem;
	width: 15rem;
}
</style>
