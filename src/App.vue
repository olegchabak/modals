<template>
	<div class="wrapper">
		<!--<header></header>-->
		<div class="wrapper-content">
			<section>
				<div class="container">
					<h1>{{title}}</h1>
					<modal title="First modal" v-if="modalFirst" @modalClose="modalFirst = false">
						<div slot="modalBody">
							<p>test</p>
							<button class="btn btnPrimary" @click="modalFirst = !modalFirst">Modal</button>
						</div>
						<div slot="modalFooter">
							<p>Modal footer</p>
						</div>
					</modal>
					<button class="btn btnPrimary" @click="modalFirst = !modalFirst">Modal</button>
				</div>
			</section>
		</div>
		<!--<footer></footer>-->
	</div>
</template>

<script>
	import modal from '@/components/Modal'
	export default {
		components: {modal},
		data(){
			return {
				title: 'My modals',
				modalFirst: false
			}
		},
		methods:{}
	}
</script>

<style>
</style>
