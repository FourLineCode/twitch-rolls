<template>
	<div id="panel">
		<p>{{ title }}</p>
		<form id="form">
			<div>
				<label for="game">Game</label>
				<input v-model="game" type="text" name="game" />
			</div>
			<div>
				<label for="amount">Amount</label>
				<input v-model="limit" type="number" name="amount" />
			</div>
			<div>
				<button @click.prevent="rollStreams()">Roll</button>
			</div>
		</form>
	</div>
</template>

<script>
import fetch from "node-fetch"

export default {
	name: "panel",
	props: ["title"],
	data() {
		return {
			msg: "hello",
			game: "",
			amount: 3,
			limit: 5,
			offset: 0,
			streams: [],
		}
	},
	methods: {
		rollStreams() {
			const CLIENT_ID = process.env.VUE_APP_CLIENT_ID

			let game = this.game
			if (game !== "") {
				game.split(" ").join("%20")

				game = "&game=" + game
			}

			let offset = "&offset=" + this.offset
			let limit = "&limit=" + this.limit
			this.offset += this.limit

			const url =
				"https://api.twitch.tv/kraken/streams/?stream_type=live&language=en" +
				game +
				offset +
				limit

			const headers = {
				Accept: "application/vnd.twitchtv.v5+json",
				"Client-ID": CLIENT_ID,
			}

			fetch(url, { method: "GET", headers: headers })
				.then((res) => {
					return res.json()
				})
				.then((data) => {
					this.streams = data.streams
					this.streams.forEach((stream) => {
						console.log(
							stream.channel.display_name,
							stream.viewers,
							stream.channel.game
						)
					})
				})
		},
	},
}
</script>

<style scoped>
#form {
	display: flex;
	justify-content: space-evenly;
	justify-items: center;
	text-align: center;
	flex-direction: column;
	height: 100%;
	width: 300px;
}

#form div {
	display: flex;
	justify-content: space-evenly;
	margin: 10px auto;
}
</style>
