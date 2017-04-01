<template>
	<div class="toast" :class="{ isActive: active, 'toast--snackbar': persistent }">

		<div class="toast-container background--dark foreground--primaryLight">

			<div class="toast-message">
				{{ message }}
			</div>

			<div class="toast-action">
				<md-button type="inline" accent="secondary" @clicked="triggerClick">{{ action }}</md-button>
			</div>

		</div>

	</div>
</template>

<script>
import mdButton from '../md-button/md-button.vue';

export default {
	components: {
		'md-button': mdButton
	},
	props: {
		message: { required: true },
		active: { required: true },
		action: { required: false },
		trigger: { required: false },
		persistent: { default: false }
	},
	methods: {
		triggerClick() {
			this.trigger();
		}
	}
}
</script>


<style>

.toast {
	position: fixed;

	width: 100%;

	left: 0;
	bottom: -5em;

	transform: bottom;
	transition-duration: 0.4s;
	transition-property: bottom;
}

.toast.isActive {
	bottom: 1em;
}

.toast-container {
	display: flex;
	border-radius: 0.2em;

	padding-left: 1.5em;
	padding-right: 1.5em;

	line-height: 3em;

	min-width: 288px;
	max-width: 568px;

	margin-left: auto;
	margin-right: auto;
}


.toast-message {
	flex: 8;
}

.toast-action {
	flex: 1;
}

.toast--snackbar.isActive {
	bottom: 0;
}

.toast--snackbar .toast-container {
	border-radius: 0;

	min-width: initial;
	max-width: initial;
	width: 100%;
}

</style>