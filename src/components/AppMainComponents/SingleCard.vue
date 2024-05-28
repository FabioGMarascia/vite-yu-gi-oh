<script>
export default {
	name: "SingleCard",
	props: { element: Object },
};
</script>

<template>
	<div class="col-2 mx-2 mb-3 px-0">
		<img :src="element.card_images[0].image_url" />

		<div class="cardInfoBox text-center py-4">
			<h2 class="text-white fw-bold">{{ element.name }}</h2>
			<span>{{ element.archetype }}</span>
		</div>
	</div>
</template>

<style scoped>
img {
	width: 100%;
}

.cardInfoBox {
	background-color: #d48f38;
}

h2 {
	font-size: 1rem;
}
</style>
