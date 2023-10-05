<template>
	<div class="text" :class="{ 'has-header': showHeader }">
		{{ text }}
		<img class="dog-img" :src="currentDog" />
	</div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
	props: {
		showHeader: {
			type: Boolean,
			default: false,
		},
		text: {
			type: String,
			default: '',
		},
	},
	data: () => ({
		currentDog: "",
		currentDogName: "",
	}),
	async mounted() {
		var dog = await fetch("https://api.thedogapi.com/v1/images/search?limit=10");
		dog = await dog.json();
		this.currentDog = dog[0].url;
	}
});
</script>

<style scoped>
.text {
	padding: 12px;
}

.dog-img {
	width: 100%;
}

.dog-name {
	text-align: center;
	font-size: 1.5rem;
	font-weight: bold;
	color: rgb(71, 209, 255);
}

.text.has-header {
	padding: 0 12px;
}
</style>
