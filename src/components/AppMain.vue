<script>
import CardList from "./AppMainComponents/CardList.vue";

export default {
	name: "AppMain",
	components: {
		CardList,
	},
};
</script>

<template>
	<div class="mainBox py-4 deb">
		<select class="form-select ms-5 mb-4 deb">
			<option selected>Open this select menu</option>
			<option value="1">Alien</option>
			<option value="2">Two</option>
			<option value="3">Three</option>
		</select>
		<CardList />
	</div>
</template>

<style scoped>
.mainBox {
	background-color: #d48f38;
	padding: 0 12rem;
}

select {
	margin-left: 8rem;
	width: 15rem;
}
</style>
