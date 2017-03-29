<template>
	<div class="button" :class="typeClass" @click="triggerClick">
		<md-ripple :accent="rippleAccent"></md-ripple>
		<slot></slot>
	</div>
</template>

<script>
import mdRipple from '../md-ripple/md-ripple.vue';

export default {
	components: {
		'md-ripple': mdRipple
	},
	props: {
		type: { default: 'default' },
		action: { required: false },
		accent: { default: 'default' }
	},
	data() {
		return {
			typeClass: '',
			rippleAccent: ''
		};
	},
	mounted() {
		let rippleAccent = this.accent;
		if (this.accent == 'default')
			rippleAccent = 'dark';

		if (this.type != 'flat') {
			if (this.accent != 'default')
				rippleAccent += 'Alternate';

			this.typeClass = [ 'background--'+this.accent, 'foreground--'+this.accent+'Alternate', 'raise--1'];
			this.rippleAccent = rippleAccent;
		} else {
			this.typeClass = [ 'foreground--'+this.accent ];
			this.rippleAccent = rippleAccent;
		}

	},
	methods: {
		triggerClick(e) {
			this.$emit('clicked');
		}
	}
}
</script>


<style>
.button {
	cursor: pointer;
	display: inline-block;

	position: relative;

	line-height: 1.5em;

	padding-left: 0.5em;
	padding-right: 0.5em;

	border-radius: 0.2em;

	overflow: auto;
}
</style>
