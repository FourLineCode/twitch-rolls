<template>
	<div id="panel">
		<v-content>
			<v-container class="fill-height" fluid>
				<v-row align="center" justify="center">
					<v-col cols="12" sm="8" md="4">
						<v-card class="elevation-12">
							<v-toolbar color="purple" dark flat>
								<v-icon left>casino</v-icon>
								<v-toolbar-title>Twitch Rolls</v-toolbar-title>
							</v-toolbar>
							<v-card-text>
								<v-form>
									<v-text-field
										label="Game"
										name="game"
										prepend-icon="sports_esports"
										type="text"
										v-model="game"
									></v-text-field>

									<v-text-field
										label="Amount"
										name="amount"
										prepend-icon="people_outline"
										type="number"
										v-model="limit"
									></v-text-field>
								</v-form>
							</v-card-text>
							<v-card-actions>
								<v-spacer></v-spacer>
								<v-btn dark color="purple" @click="rollStreams()"
									><v-icon left>rotate_left</v-icon>Roll<v-icon right
										>rotate_right</v-icon
									></v-btn
								>
								<v-spacer></v-spacer>
							</v-card-actions>
						</v-card>
					</v-col>
				</v-row>
			</v-container>
		</v-content>
		<v-item-group>
			<v-container class="pa-0">
				<v-row class="d-flex justify-center">
					<v-col
						v-for="stream in this.streams"
						:key="stream.id"
						cols="12"
						md="4"
					>
						<v-item>
							<card v-bind:stream="stream"></card>
						</v-item>
					</v-col>
				</v-row>
			</v-container>
		</v-item-group>
	</div>
</template>

<script>
import fetch from "node-fetch"
import Card from "./Card"

export default {
	name: "panel",
	props: ["title"],
	components: {
		card: Card,
	},
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
				})
		},
	},
}
</script>

<style scoped>
#panel {
	height: 100%;
}
</style>
