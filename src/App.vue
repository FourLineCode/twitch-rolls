<template>
	<div id="app">
		<panel title="Roll for random Twitch Streams"></panel>
	</div>
</template>

<script>
import Panel from "./components/Panel"

export default {
	name: "App",
	components: {
		panel: Panel,
	},
}
</script>

<style>
#app {
	font-family: sans-serif;
}
</style>
