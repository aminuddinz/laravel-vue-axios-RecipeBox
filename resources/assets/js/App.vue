<template>
	<div class="container">
		<div class="navbar">
			<div class="navbar__brand">
				<router-link to="/">Recipe Box</router-link>
			</div>
			<ul class="navbar__list">
				<li class="navbar__item" >
					<router-link to="/login">LOGIN</router-link>
				</li>
				<li class="navbar__item" >
					<router-link to="/register">REGISTER</router-link>
				</li>
				<li class="navbar__item" >
					<router-link to="/recipes/create">CREATE RECIPE</router-link>
				</li>
				<li class="navbar__item" >
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
import Flash from './helpers/flash.js'

export default {
  data() {
	  return {
			flash: Flash.state 
	  }
  }
}
</script>
