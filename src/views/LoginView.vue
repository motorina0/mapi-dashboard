<!-- @format -->

<template>
	<v-container fill-height fluid>
		<v-row justify="center">
			<v-col class="d-flex justify-center">
				<v-card elevation="12" min-width="300" width="500" color="secondary">
					<v-toolbar color="primary">
						<v-toolbar-title>LNbits Dashboard</v-toolbar-title>
						<v-spacer />
					</v-toolbar>
					<v-card-text>
						<v-form>
							<v-text-field
								ref="domain"
								v-model="domain"
								:rules="[() => !!domain || 'This field is required']"
								prepend-icon="mdi-account"
								label="Domain"
								placeholder="legend.lnbits.com"
								required
							/>
							<v-text-field
								ref="readKey"
								v-model="readKey"
								:rules="[() => !!readKey || 'This field is required']"
								:append-icon="showPassword ? 'mdi-eye-off' : 'mdi-eye'"
								:type="showPassword ? 'text' : 'password'"
								prepend-icon="mdi-lock"
								label="Invoice/read key"
								placeholder="*********"
								counter
								required
								@keydown.enter="login"
								@click:append="showPassword = !showPassword"
							/>
						</v-form>
					</v-card-text>
					<v-divider class="mt-5" />
					<v-card-actions>
						<v-spacer />
						<v-btn align-center justify-center color="tertiary" @click="login"> Login </v-btn>
					</v-card-actions>
					<v-snackbar v-model="snackbar" :color="color" :top="true">
						{{ errorMessages }}
						<v-btn text @click="snackbar = false"> Close </v-btn>
					</v-snackbar>
				</v-card>
			</v-col>
		</v-row>
	</v-container>
</template>

<script>
	export default {
		name: 'LoginView',
		data: function () {
			return {
				readKey: '',
				domain: '',
				errorMessages: 'Incorrect auth info',
				snackbar: false, // this is the wrong pass notification
				color: 'general',
				showPassword: false,
			}
		},

		// Sends action to Vuex that will log you in and redirect to the dash otherwise, error
		//needs to finish implementing using the states in mutations
		methods: {
			login: function () {
				let readKey = this.readKey
				let domain = this.domain
				this.$store
					.dispatch('login', {readKey, domain }) //calls the login action and passes login info
					.then(() => this.$router.push('/')) //redirect to dash after login
					.catch((err) => {
						console.log(err)
						this.snackbar = true //shows error on wrong pass
					})
			},
		},
		metaInfo() {
			return {
				title: 'LNbits Auth',
			}
		},
	}
</script>
