<template>
<body>
	<header>
		<h1>Dice Rolling</h1>
	</header>
	<main>
		<ul class="dice">
			<li v-for="group in diceGroups" :key="group.id">
				<DiceGroup @delete="deleteGroup(group)"/>
			</li>
			<li class="add-group-button__container">
				<button class="add-group-button" @click="addGroup">Add group</button>
			</li>
		</ul>
	</main>
</body>
</template>

<script>
import DiceGroup from "./DiceGroup.vue";
export default {
	components: { DiceGroup },
	data() {
		return {
			diceGroups: [
				{
					id: new Date().toString()
				}
			]
		};
	},
	methods: {
		addGroup() {
			this.diceGroups.push({
				id: new Date().toString()
			});
		},
		deleteGroup(group) {
			this.diceGroups = this.diceGroups.filter(
				ogGroup => ogGroup.id !== group.id
			);
		}
	},
	name: "App"
};
</script>

<style>
body {
	margin: 0;
	padding: 16px;
}
</style>
