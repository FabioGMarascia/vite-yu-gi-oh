<script>
import SingleCard from "./SingleCard.vue";
import store from "../../data/store.js";

export default {
	name: "CardList",
	components: {
		SingleCard,
		store,
	},
	props: ["item"],
	data() {
		return {
			store,
		};
	},
};
</script>

<template>
	<div class="row mx-0 justify-content-between">
		<SingleCard v-for="card in store.cards" :element="card" />
	</div>
</template>

<style scoped></style>
