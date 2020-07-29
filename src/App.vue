<template>
	<div class="wrapper">
		<!--<header></header>-->
		<div class="wrapper-content">
			<section>
				<div class="container">
					<h1>{{title}}</h1>
					
					<!--First modal-->
					<modal title="First modal" v-show="modalFirst" @modalClose="modalFirst = false">
						<div slot="modalBody">
							<p>test</p>
							<button class="btn btnPrimary" @click="modalFirst = !modalFirst">First Modal</button>
						</div>
						<div slot="modalFooter">
							<p>Modal footer</p>
						</div>
					</modal>
					<button class="btn btnPrimary" @click="modalFirst = !modalFirst">First Modal</button>
					
					<!--Second modal-->
					<modal title="Modal with form" v-show="modalSecond.show" @modalClose="modalSecond.show = false">
						<div slot="modalBody">
							<form @submit.prevent="submitSecondForm">
								<label for="inputName">Your name:</label>
								<input id="inputName" required type="text" v-model="modalSecond.name">
								<label for="inputEmail">Your email:</label>
								<input id="inputEmail" required type="email" v-model="modalSecond.email">
								<button class="btn btnPrimary">Submit</button>
							</form>
						</div>
						<div slot="modalFooter"></div>
					</modal>
					<button class="btn btnPrimary" @click="modalSecond.show = !modalSecond.show">Modal with form</button>

					<!--modal with Validate-->
					<button class="btn btnPrimary" @click="modalValidate = !modalValidate">Modal with validate</button>
					<modal-validate
							v-show="modalValidate" @modalClose="modalValidate = false"
					></modal-validate>

				</div>
			</section>
		</div>
		<!--<footer></footer>-->
	</div>
</template>

<script>
	import modal from '@/components/UI/Modal'
	import modalValidate from '@/components/ModalValidate'

	export default {
		components: {modal, modalValidate},
		data(){
			return {
				title: 'My modals',
				modalFirst: false,
				modalSecond: {
					show: false,
					name: '',
					email: ''
				},
				modalValidate: false
			}
		},
		methods:{
			submitSecondForm() {
				console.log({
					name: this.modalSecond.name,
					email: this.modalSecond.email
				});
				this.modalSecond.name = '';
				this.modalSecond.email = '';
				this.modalSecond.show = false;

			}
		}
	}
</script>

<style lang="scss">
	.btn {
		margin-right: 15px;
	}
</style>
