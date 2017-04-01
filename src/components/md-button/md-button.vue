<template>
	<div class="button" :class="typeClass" @click="triggerClick">
		<md-ripple :accent="rippleAccent" />
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
		this.setAccent();
	},
	methods: {
		setAccent() {
			this.rippleAccent = this.accent == 'default' ? 'dark' : (this.type == 'default' ? this.accent+'Alternate' : this.accent);

			if (this.type == 'default')
				this.typeClass = [ 'background--'+this.accent, 'foreground--'+this.accent+'Alternate', 'raise--1' ];
			else
				this.typeClass = [ 'foreground--'+this.accent ];
		},

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

	line-height: 2em;

	padding-left: 0.5em;
	padding-right: 0.5em;

	border-radius: 0.2em;

	overflow: auto;
}
</style>
