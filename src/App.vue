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
			cardUrl: "https://db.ygoprodeck.com/api/v7/cardinfo.php?num=2000&offset=0",
			archetypeUrl: "https://db.ygoprodeck.com/api/v7/archetypes.php",
			selected: "",
			store,
			allCards: [],
			checkScroll: false,
		};
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
		backToTop() {
			window.scrollTo({
				top: 0,
				behavior: "smooth",
			});
		},
		handleScroll() {
			if (window.scrollY > 20) {
				this.checkScroll = true;
				console.log(`ciao`);
			} else {
				this.checkScroll = false;
			}
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
	mounted() {
		window.addEventListener(`scroll`, this.handleScroll);
	},
};
</script>

<template>
	<AppHeader />
	<div class="mainBox py-4">
		<div class="col-2 px-0 mb-4 mx-auto">
			<select class="fw-bold w-100 text-center" v-model="selected" @change="getAcrchetype">
				<option value="">Select the archetype</option>
				<option v-for="archetype in store.archetypeList">
					{{ archetype.archetype_name }}
				</option>
			</select>
		</div>

		<AppMain />

		<button
			type="button"
			class="btn btn-danger btn-lg position-fixed"
			id="btn-scroll-top"
			v-if="checkScroll"
			@click="backToTop">
			<i class="fas fa-arrow-up"></i>
		</button>
	</div>
</template>

<style scoped>
.mainBox {
	background-color: #d48f38;
	padding: 0 12rem;
}

#btn-scroll-top {
	bottom: 20px;
	right: 20px;
}
</style>
