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
			cardUrl: "https://db.ygoprodeck.com/api/v7/cardinfo.php?num=300&offset=0",
			archetypeUrl: "https://db.ygoprodeck.com/api/v7/archetypes.php",
			selected: "",
			store,
			allCards: [],
		};
	},
	methods: {
		getAcrchetype() {
			setTimeout(() => {
				if (this.selected != "") {
					axios
						.get("https://db.ygoprodeck.com/api/v7/cardinfo.php?archetype=" + this.selected)
						.then((result) => {
							this.store.cards = result.data.data;
						});
				} else {
					this.store.cards = this.allCards;
				}
			}, 1);
		},
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
};
</script>

<template>
	<AppHeader />
	<div class="mainBox py-4">
		<div class="col-2 px-0 mb-4 mx-auto">
			<select class="form-select fw-bold w-100" v-model="selected" @input="getAcrchetype">
				<option value="">Select the archetype</option>
				<option v-for="archetype in store.archetypeList">
					{{ archetype.archetype_name }}
				</option>
			</select>
		</div>

		<AppMain />
	</div>
</template>

<style scoped>
.mainBox {
	background-color: #d48f38;
	padding: 0 12rem;
}
</style>
