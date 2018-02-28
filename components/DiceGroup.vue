<template>
	<li class="group">
		<div class="name">
			<label>
				Name: 
				<input type="text" v-model="name">
			</label>
		</div>
		<div class="quantity">
			<label>
				Quantity: 
				<input v-model="quantity" type="number" min="0">
			</label>
		</div>
		<div class="range">
			<label>
				Min:
				<input v-model="minimum" type="number" min="0">
			</label>
			<label>
				Max:
				<input v-model="maximum" type="number" :min="minimum + 1">
			</label>
		</div>
		<div class="roll__container">
			<button class="results__button" @click="rollDice">Roll!</button>
		</div>
		<div class="results__container" v-if="results.length">
			<h3 class="results__title">Results</h3>
			<ul class="results">
				<li class="results__item" v-for="result in results" :key="result.id">
					{{result.number}}
				</li>
			</ul>
		</div>
		<div class="delete-button__container">
			<button class="delete-button" @click="deleteGroup">Delete Group</button>
		</div>
	</li>
</template>

<script>
export default {
	data() {
		return {
			maximum: 6,
			minimum: 1,
			name: "Move Spaces",
			quantity: 1,
			results: []
		};
	},
	methods: {
		decrement(field) {
			field += 1;
		},
		deleteGroup() {
			this.$emit("delete");
		},
		increment(field) {
			if (field > 1) {
				field -= 1;
			}
		},
		rollDice() {
			this.results = [];
			for (let i = 0; i < this.quantity; ++i) {
				let result = {
					id: new Date().toString(),
					number: getRandomInt(this.minimum, this.maximum)
				};
				console.log(result);
				this.results.push(result);
			}
		}
	},
	name: "DiceGroup"
};

function getRandomInt(min, max) {
	return Math.floor(Math.random() * (max - min + 1)) + min;
}
</script>

<style>

</style>
