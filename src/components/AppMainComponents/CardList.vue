<script>
import SingleCard from "./SingleCard.vue";
import store from "../../data/store.js";

export default {
	name: "CardList",
	components: {
		SingleCard,
	},
	data() {
		return {
			store,
		};
	},
};
</script>

<template>
	<div class="listBox p-5">
		<div class="foundBox p-4 text-white mx-2 mt-2 fw-bold fs-6">
			Found {{ store.cards.length }} cards
		</div>

		<div class="row mx-0 justify-content-between">
			<SingleCard v-for="card in store.cards" :element="card" />
		</div>
	</div>
</template>

<style scoped>
.listBox {
	background-color: white;
}

.foundBox {
	background-color: black;
}
</style>
