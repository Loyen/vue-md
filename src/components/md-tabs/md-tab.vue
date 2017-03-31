<template>
	<div class="tabs-content background--primaryAlternate" :class="{ isActive }">

		<slot></slot>

	</div>
</template>

<script>
export default {
	props: {
		name: { required: true },
		selected: { default: false }
	},
	data() {
		return {
			isActive: false
		};
	},
	mounted() {
		this.isActive = this.selected;

		this.$parent.setTab(this);
	}
}
</script>


<style>

.tabs-content {
	display: none;
}


.tabs-content.isActive {
	display: block;
}

</style>