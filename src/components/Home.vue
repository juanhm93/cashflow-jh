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
				<template #graphic> <Graphic :amounts="amounts" /> </template>
				<template #action> <Action /> </template>
			</Resume>
		</template>
		<template #movements>
			<Movements :movements="movements" />
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
			totalAmount: 75000,
			label: null,
			labelTotal: "Ahorro total",
			amounts: [100, 200, 500, 200, -400, -600, -300, 0, 300, 500],
			specificDate: new Date(),
			movements: [
				{
					id: 0,
					title: "Movimiento 1",
					description: "primer movimiento",
					amount: 100,
				},
				{
					id: 1,
					title: "Movimiento 2",
					description: "segundo movimiento",
					amount: 200,
				},
				{
					id: 2,
					title: "Movimiento 3",
					description: "tercero movimiento",
					amount: 500,
				},
				{
					id: 3,
					title: "Movimiento 4",
					description: "cuarto movimiento",
					amount: 200,
				},
				{
					id: 4,
					title: "Movimiento 5",
					description: "quinto movimiento",
					amount: -400,
				},
				{
					id: 5,
					title: "Movimiento 6",
					description: "sexto movimiento",
					amount: -600,
				},
				{
					id: 6,
					title: "Movimiento 7",
					description: "septimo movimiento",
					amount: -300,
				},
				{
					id: 7,
					title: "Movimiento 8",
					description: "octavo movimiento",
					amount: 0,
				},
				{
					id: 8,
					title: "Movimiento 9",
					description: "noveno movimiento",
					amount: 300,
				},
				{
					id: 9,
					title: "Movimiento 10",
					description: "decimo movimiento",
					amount: 500,
				},
			],
		};
	},
};
</script>
