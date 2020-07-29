<template>
	<transition name="modal">
		<div class="modal__wrapper" @click="$emit('modalClose')">
			<div class="modal-content" @click.stop>
				<div class="modal-header">
					<div class="modal-title">{{title}}</div>
					<!--напрямую эмитит событие, минуя создание метода-->
					<button class="button-close" @click="$emit('modalClose')">x</button>
				</div>
				<div class="modal-body">
					<slot name="modalBody">
						Default body
					</slot>
					<slot name="modalFooter">Default modal footer</slot>
				</div>
			</div>
		</div>
	</transition>
</template>

<script>
	export default {
		name: "Modal",
		props: {
			title: {
				type: String,
				required: true
			}
		},
		data(){
			return {
				showModal: true
			}
		},
		mounted() {
			document.body.addEventListener('keyup', event => {
				if (event.keyCode === 27) this.$emit('modalClose')
			});
		}
	}
</script>

<style lang="scss">
	@import "src/assets/scss/common/buttons";
	.modal__wrapper{
		display: flex;
		justify-content: center;
		align-items: center;
		position: fixed;
		top: 0;
		bottom: 0;
		left: 0;
		transition: opacity .2s ease;
		right: 0;
		z-index: 998;
		background-color: rgba(00,00,00,.48);
	}

	.modal-content {
		position: relative;
		max-width: 600px;
		padding: 20px 18px;
		background-color: #fff;
		border: 1px solid #dcdfe6;
		transition: all .2s ease;
		border-radius: 8px;
		z-index: 999;
		overflow: hidden;
		@media screen and (min-width: 900px) {
			min-width: 500px;
		}
	}
	.modal-header {
		display: flex;
		align-self: center;
		justify-content: space-between;
		padding-bottom: 20px;
		span {
			font-size: 24px;
		}
		.button-close {
			cursor: pointer;
		}
	}
	.modal-body {
		text-align: center;
	}

	.modal-enter, .modal-leave-active {
		opacity: 0;
	}
	.modal-enter .modal-content,
	.modal-leave-active .modal-content {
		transform: scale(1.2);
	}
</style>