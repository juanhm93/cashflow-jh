<template>
	<Layout>
		<template #header>
			<Header></Header>
		</template>
		<template #resume>
			<Resume
				:label="label"
				:total-label="labelTotal"
				:amount="amount"
				:total-amount="totalAmount"
				:selected-date="specificDate"
			>
				<template #graphic>
					<Graphic :amounts="amounts" @select="select" />
				</template>
				<template #action> <Action @create="create" /> </template>
			</Resume>
		</template>
		<template #movements>
			<Movements :movements="movements" @remove="remove" />
		</template>
	</Layout>
	<!-- <div>Hola Mundo</div> -->
</template>
<script>
import Layout from "./Layout.vue";
import Header from "./Header.vue";
import Resume from "./Resume/Index.vue";
import Action from "./Action.vue";
import Movements from "./Movements/Index.vue";
import Graphic from "./Resume/Graphic.vue";

export default {
	name: "Home",
	components: {
		Layout,
		Header,
		Resume,
		Action,
		Movements,
		Graphic,
	},
	data() {
		return {
			amount: null,
			label: null,
			labelTotal: "Ahorro total",
			// amounts: [100, 200, 500, 200, -400, -600, -300, 0, 300, 500],
			specificDate: new Date(),
			movements: [],
		};
	},
	computed: {
		amounts() {
			const lastDays = this.movements
				.filter((m) => {
					const today = new Date();
					const oldDate = today.setDate(today.getDate() - 30);

					return m.time > oldDate;
				})
				.map((m) => m.amount);

			return lastDays.map((m, i) => {
				const lastMovements = lastDays.slice(0, i + 1);

				return lastMovements.reduce((suma, movement) => {
					return suma + movement;
				}, 0);
			});
		},
		totalAmount() {
			return this.movements.reduce((sum, m) => {
				return sum + m.amount;
			}, 0);
		},
	},
	mounted() {
		const movements = JSON.parse(localStorage.getItem("movements"));
		if (Array.isArray(movements)) {
			this.movements = movements?.map((m) => {
				return { ...m, time: new Date(m.time) };
			});
		}
	},
	methods: {
		create(movements) {
			this.movements.push(movements);
			this.save();
		},
		remove(id) {
			const index = this.movements.findIndex((m) => m.id === id);
			this.movements.splice(index, 1);
			this.save();
		},
		save() {
			localStorage.setItem("movements", JSON.stringify(this.movements));
		},
		select(amount) {
			this.amount = amount;
		},
	},
};
</script>
