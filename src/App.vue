<template>
	<v-app>
		<panel class="purple lighten-3" title="Twitch Rolls App"></panel>
	</v-app>
</template>

<script>
import Panel from "./components/Panel"

export default {
	name: "App",

	components: {
		panel: Panel,
	},

	data: () => ({
		//
	}),
}
</script>
