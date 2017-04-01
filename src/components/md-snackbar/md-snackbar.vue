<template>
	<div class="snackbar" :class="[ { isActive: active }, 'snackbar--'+position ]">

		<div class="snackbar-container background--dark foreground--primaryLight">

			<div class="snackbar-message">
				<p>{{ message }}</p>
			</div>

			<div class="snackbar-action">
				<md-button type="flat" accent="secondary" @clicked="triggerClick">{{ action }}</md-button>
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
		position: { default: 'center' }
	},
	methods: {
		triggerClick() {
			this.trigger();
		}
	}
}
</script>


<style>

.snackbar {
	position: fixed;

	width: 100%;

	left: 0;
	bottom: -5em;

	transform: bottom;
	transition-duration: 0.4s;
	transition-property: bottom;
}

.snackbar.isActive {
	bottom: 1em;
}

.snackbar-container {
	display: flex;
	border-radius: 0.2em;

	padding-left: 1.5em;
	padding-right: 1.5em;

	line-height: 3em;

	min-width: 288px;
	max-width: 568px;
}

.snackbar-message {
	flex: 8;
}

.snackbar-action {
	flex: 1;
}

.snackbar--left .snackbar-container {
	margin-left: 1em;
}

.snackbar--center .snackbar-container {
	margin-left: auto;
	margin-right: auto;

	border-bottom-left-radius: 0;
	border-bottom-right-radius: 0;
}

.snackbar--right .snackbar-container {
	margin-left: auto;
	margin-right: 1em;
}

.snackbar.isActive.snackbar--center {
	bottom: 0;
}

</style>