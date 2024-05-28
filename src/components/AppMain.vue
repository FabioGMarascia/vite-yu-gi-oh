<script>
import CardList from "./AppMainComponents/CardList.vue";
import FoundBar from "./AppMainComponents/FoudBar.vue";

export default {
	name: "AppMain",
	components: {
		CardList,
		FoundBar,
	},
	data() {
		return {};
	},
};
</script>

<template>
	<div class="listBox p-5">
		<FoundBar />
		<CardList />
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
