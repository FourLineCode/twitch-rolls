<template>
	<v-card max-width="344" class="mx-auto">
		<v-list-item>
			<v-list-item-avatar color="grey">
				<v-img v-bind:src="stream.channel.logo"></v-img>
			</v-list-item-avatar>
			<v-list-item-content>
				<a v-bind:href="stream.channel.url">
					<v-list-item-title class="headline">{{
						stream.channel.display_name
					}}</v-list-item-title>
				</a>
				<v-list-item-subtitle>
					<span
						>Playing
						<span class="blue--text">{{ stream.channel.game }}</span></span
					>
				</v-list-item-subtitle>
			</v-list-item-content>
		</v-list-item>

		<a v-bind:href="stream.channel.url">
			<v-img v-bind:src="stream.preview.medium" height="180"></v-img
		></a>

		<span class="d-flex justify-space-around red--text">
			<span
				><v-icon small color="red">fiber_manual_record</v-icon>
				{{ stream.viewers }}</span
			>
		</span>
	</v-card>
</template>

<script>
export default {
	props: ["stream"],
}
</script>

<style scoped>
a {
	text-decoration: none;
	color: purple;
}

img:hover {
	cursor: pointer;
}
</style>
