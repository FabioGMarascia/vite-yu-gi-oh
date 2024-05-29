<script>
import store from "../../data/store.js";

export default {
	name: "FoundBar",
	components: {
		store,
	},
	data() {
		return {
			store,
		};
	},
};
</script>

<template>
	<div class="foundBox p-4 text-white mx-2 mt-2 fw-bold fs-6">
		Found {{ store.cards.length }} cards
	</div>
</template>

<style scoped></style>
