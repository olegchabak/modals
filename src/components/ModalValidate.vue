<template>
	<modal title="Modal with validate" @modalClose="$emit('modalClose')">
		<div slot="modalBody">
			<form @submit.prevent="onSubmit">
				<div class="form-item" :class="{'form-item--error': $v.name.$error}">
					<label for="inputName">Your name:</label>
					<input id="inputName" v-model="name" :class="{error: $v.name.$error}" @change="$v.name.$touch()">
					<p class="error-text" v-if="!$v.name.required">Field is required</p>
					<p class="error-text" v-if="!$v.name.alpha">The field must contain only letters</p>
					<p class="error-text" v-if="!$v.name.minLength">The field must contain at least {{$v.name.$params.minLength.min}} characters</p>
				</div>
				<div class="form-item" :class="{'form-item--error': $v.email.$error}">
					<label for="inputEmail">Your email:</label>
					<input
						id="inputEmail"
						v-model="email"
						:class="{error: $v.email.$error}"
						@change="$v.email.$touch()"
					>
					<p class="error-text" v-if="!$v.email.required">Field is required</p>
					<p class="error-text" v-if="!$v.email.alpha">Invalid email address</p>
				</div>
				<button class="btn btnPrimary">Submit</button>
			</form>
		</div>
		<div slot="modalFooter"></div>
	</modal>
</template>

<script>
	import {required, minLength, email, alpha,} from 'vuelidate/lib/validators';
	import modal from '@/components/UI/Modal';

	export default {
		name: "modal-validate",
		components: {modal},
		validations: {
			name: {required, alpha, minLength: minLength(2)},
			email: {email, required}
		},
		data() {
			return {
				name: '',
				email: ''
			}
		},
		methods: {
			onSubmit() {
				this.$v.$touch();
				if (!this.$v.$invalid) {
					const user = {
						name: this.$v.name.$model,
						email: this.$v.email.$model
					}
					console.log(user)

					// done!
					this.$v.name.$model = ''
					this.$v.email.$model = ''
					this.$v.$reset()
					this.$emit('modalClose')
				}
			}
		}

	}
</script>

<style lang="scss">
	.form-item {
		margin-bottom: 30px;
		&--error {
			color: red;
			.error-text {
				display: block;
			}
		}
		input {
			margin-bottom: 5px;
			&.error {
				border-color: rgba(255, 0, 0, 0.99);
			}
		}

	}
	.error-text {
		font-size: 13px;
		display: none;

	}


</style>