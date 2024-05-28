<script>
import AppHeader from "./components/AppHeader.vue";
import AppMain from "./components/AppMain.vue";
import store from "./data/store.js";

export default {
	name: "App",
	components: {
		AppHeader,
		AppMain,
		store,
	},
	data() {
		return {};
	},
	mounted() {
		axios.get("https://db.ygoprodeck.com/api/v7/cardinfo.php?num=10&offset=0").then((result) => {
			store.cards = result.data.data;
		});
	},
};
</script>

<template>
	<AppHeader />
	<AppMain />
</template>

<style scoped></style>
