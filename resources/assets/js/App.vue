<template>
	<div class="container">
		<div class="navbar">
			<div class="navbar__brand">
				<router-link to="/">Recipe Box</router-link>
			</div>
			<ul class="navbar__list">
				<li class="navbar__item" v-if="!checkAuth">
					<router-link to="/login">LOGIN</router-link>
				</li>
				<li class="navbar__item" v-if="!checkAuth">
					<router-link to="/register">REGISTER</router-link>
				</li>
				 <li class="navbar__item" v-if="checkAuth">
					<router-link to="/recipes/create">CREATE RECIPE</router-link>
				</li> 
				<li class="navbar__item" v-if="checkAuth" style="cursor:pointer">
					<a @click.stop="logout">LOGOUT</a>
				</li>
			</ul>
		</div>

		<div class="flash flash__success" v-if="flash.success">
			{{ flash.success }}
		</div>
		<div class="flash flash__error" v-if="flash.error">
			{{ flash.error }}
		</div>

		<router-view></router-view>

	</div>
</template>

<script>

import Flash from './helpers/flash'
import Auth from './store/auth'
import { post } from './helpers/api'

export default {

	created() {
		Auth.initialize()
	},

	data() {
		return {
				flash: Flash.state, // state from helpers/flash.js
				auth: Auth.state // state from store/auth.js
		}
	},

	computed: {
		checkAuth() {
			if(this.auth.api_token && this.auth.user_id) {
				return true
			}
			return false
		}
	},

	methods: {
		logout() {
			post('/api/logout')
			  .then( (res) => {
					if(res.data.logged_out) {
						Auth.remove() //remove data auth from local storage
						Flash.setSuccess('You have successfully logged out.') // flash message
						this.$router.push('/login') // redirect
					}
			  })
		}
	}

}
</script>
