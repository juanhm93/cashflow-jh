<template>
	<!-- <Home /> -->
	<suspense>
		<template #default>
			<Home />
		</template>
		<template #fallback>
			<SplashScreen />
		</template>
	</suspense>
</template>

<script>
import SplashScreen from "./components/SplashScreen.vue";
import { defineAsyncComponent } from "vue";

export default {
	name: "App",
	components: {
		SplashScreen,
		Home: defineAsyncComponent(() => {
			return new Promise((resolve) => {
				setTimeout(() => {
					resolve(import("./components/Home.vue"));
				}, 2500);
			});
		}),
	},
};
</script>

<style>
html,
body,
.app {
	min-height: 100vh;
	margin: 0;
	font-family: Arial, Helvetica, sans-serif;
}

* {
	--brand-green: #04b500;
	--brand-blue: #0689b0;
}
</style>
