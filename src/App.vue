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
			allCards: [],
		};
	},
	created() {
		axios.get(this.cardUrl).then((result) => {
			this.store.cards = result.data.data;
			this.allCards = this.store.cards;
		});

		axios.get(this.archetypeUrl).then((result) => {
			this.store.archetypeList = result.data;
		});
	},
	methods: {
		getAcrchetype() {
			if (this.selected != "") {
				axios
					.get("https://db.ygoprodeck.com/api/v7/cardinfo.php?archetype=" + this.selected)
					.then((result) => {
						this.store.cards = result.data.data;
					});
			} else {
				this.store.cards = this.allCards;
			}
		},
	},
};
</script>

<template>
	<AppHeader />
	<div class="mainBox py-4">
		<div class="row">
			<div class="col-3 pe-0">
				<select class="form-select mb-4 fw-bold" v-model="selected">
					<option value="">Select the archetype</option>
					<option v-for="archetype in store.archetypeList">
						{{ archetype.archetype_name }}
					</option>
				</select>
			</div>

			<div class="col-1 px-0">
				<button class="btn w-100 fw-bold bg-white" @click="getAcrchetype">SEARCH</button>
			</div>
		</div>

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
