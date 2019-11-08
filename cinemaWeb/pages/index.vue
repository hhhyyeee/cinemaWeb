<template>
	<v-container fluid ma-0 pa-0>
		<div class="page">
			<div class="content">
				<img src="https://wonderfulmind.co.kr/wp-content/uploads/2017/03/%EC%86%90%EC%97%90-%EA%B3%A0%EC%96%91%EC%9D%B4-600x409-e1535510249284.jpeg">
				<h1 class="title">
					Cinema Archive
				</h1>
				<div>
					<span v-if="!ifloggedin">
						<v-dialog
								v-model="dialog"
								width="30%"
						>
							<template v-slot:activator="{ on }">
								<v-btn
										color="red lighten-2"
										dark
										v-on="on"
								>
									Sign In
								</v-btn>
							</template>
							<v-card>
								<v-card-title
										class="headline grey lighten-2"
										primary-title
								>
									Sign In
								</v-card-title>
								<v-form class="signinForm">
									<v-text-field
											v-model="email"
											:rules="emailRules"
											label="Email"
											required
									></v-text-field>
									<v-text-field
											v-model="password"
											:append-icon="showPassword ? 'visibility' : 'visibility_off'"
											:rules="passwordRules"
											:type="showPassword ? 'text' : 'password'"
											label="Password"
											required
											@click:append="showPassword = !showPassword"
									></v-text-field>
								</v-form>
								<v-card-text class="errMsg"
											 v-if="signinErr"
								> {{ signinErrMsg }} </v-card-text>

								<v-divider></v-divider>

								<v-card-actions>
									<v-btn
											color="grey"
											text
											@click="signInSubmit(email, password)"
									>
										Sign In
									</v-btn>
								</v-card-actions>
							</v-card>
						</v-dialog>
					</span>
					<span v-else>
						<p>You're logged in.</p>
					</span>

					<span class="text-center" v-if="!ifloggedin">
						<v-btn
								color="grey"
								text
						>
							Register
						</v-btn>
					</span>
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
				signinErr: false,
				signinErrMsg: 'Oops, ID or Password is wrong',
				dialog: false,
				email: "",
                emailRules: [
                    v => !!v || 'E-mail is required',
                    v => /.+@.+/.test(v) || 'E-mail must be valid',
                ],
				password: "",
                passwordRules: [
                    v => !!v || 'Password is required',
                    v => v.length >= 8 || 'Password must be longer than 8 characters'
                ],
                showPassword: false,
			}
		},
		methods: {
			async signInSubmit(email, password) {
				await this.$axios.$post(
						'http://localhost:3030/api/auth/signin',
						{
							email: email,
							password: password
						})
						.then((response) => {
                            console.log(">> post result <<")
							console.log(response)
							this.dialog = false
							this.$router.push('/')
						})
						.catch((error) => {
							this.email = ''
							this.password = ''
							this.signinErr = true
						})
			},
		},
        async asyncData({ $axios }) {
            const cookies = await $axios.$get('http://localhost:3030/api/auth/signedstatus')
			console.log(">> signedstatus <<")
			console.log(cookies.email)
            return {
                ifloggedin: cookies.email
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
	background-color: #3A3936;
}
.content {
	background-color: #FFFDF9;
	width: 80%;
	height: 60vh;
	margin: auto;
}
.signinForm {
    margin: 5%;
}
.errMsg {
	color: #d0021b;
	font-size: 0.8em;
}
</style>

