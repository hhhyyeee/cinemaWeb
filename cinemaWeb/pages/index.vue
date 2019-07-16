<template>
	<v-container fluid ma-0 pa-0>
		<div class="page">
			<div class="content">
				<img src="https://wonderfulmind.co.kr/wp-content/uploads/2017/03/%EC%86%90%EC%97%90-%EA%B3%A0%EC%96%91%EC%9D%B4-600x409-e1535510249284.jpeg">
				<h1 class="title">
					Cinema Archive
				</h1>
				<div>
					<v-btn v-on:click="counter += 1">Add 1</v-btn>
					<p>The button above has been clicked {{ counter }} times.</p>
				</div>
			</div>
				<v-btn class="btn-down" @click="$vuetify.goTo('#test')">
					<i class="material-icons md-48">arrow_downward</i>
				</v-btn>
		</div>
		<div id="test" class="page">
			<div class="content">
				<p>Test</p>
			</div>
		</div>
	</v-container>
</template>

<script>
	import AppLogo from '~/components/AppLogo.vue'

	export default {
		data () {
			return {
				counter: 0,
			}
		},
		computed: {
		},
		components: {
			AppLogo
		}
	}
	
</script>

<style>
.container {
	display: block;
	justify-content: center;
	align-items: center;
	text-align: center;
}
.title {
	font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif; /* 1 */
	display: block;
	font-weight: 600;
	font-size: 2em;
	color: #35495e;
	letter-spacing: 1px;
	padding-top: 15px;
}
.subtitle {
	font-weight: 300;
	font-size: 1em;
	color: #526488;
	word-spacing: 5px;
	padding-bottom: 15px;
}
.btn-down {
	color: #FFFDF9;
	/*font-family: "Roboto", "san-serif";*/
	font-size: 18px;
}
.links {
	padding-top: 15px;
}
.page {
	height: 100vh;
	border: solid thin;
	background-color: #252420;
}
.content {
	background-color: #FFFDF9;
	margin: 1em;
	padding: 1em;
}
</style>

