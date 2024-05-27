<script>
import SingleCard from "./SingleCard.vue";

export default {
	name: "CardList",
	components: {
		SingleCard,
	},
};
</script>

<template>
	<div class="listBox row mx-0 p-5">
		<SingleCard />
	</div>
</template>

<style scoped>
.listBox {
	background-color: white;
}
</style>
