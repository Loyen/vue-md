<template>
	<div>
		<div class="textfield foreground--dark border--dark" :class="{ isTouched: focus || hasText() }">
			<div class="textfield-label">{{ label }}</div>
			<textarea :rows="rowCount()" class="textfield-input" v-model="text" @focus="focus = true" @blur="focus = false" @input="cleanText()"></textarea>
			<div v-if="description" class="textfield-helper">{{ description }}</div>
		</div>
	</div>
</template>

<script>
export default {
	props: {
		label: { default: '' },
		description: { description: '' },
		required: { default: false },
		multiline: { default: false }
	},
	data() {
		return {
			text: '',
			focus: false,
			classes: ''
		}
	},
	methods: {
		hasText() {
			return this.text.length > 0;
		},
		rowCount() {
			if (!this.multiline) return 1;

			let text_split = this.text.split(/\r\n|\r|\n/);
			return text_split.length;
		},
		cleanText() {
			if (!this.multiline)
				this.text = this.text.replace(/\r\n|\r|\n/gm, '');
		}
	}
}
</script>


<style>
.textfield {
	position: relative;

	font-size: 1em;
	line-height: 1.2em;

	transition-property: padding-top;
	transition-duration: 0.1s;
	transition-timing-function: linear;

	margin-bottom: 0.4em;
}

.textfield-label {
	margin-top: 0.4em;
	padding-left: 0.1em;
	line-height: inherit;

	position: absolute;
	transition-property: font-size,margin-top;
	transition-duration: inherit;
	transition-timing-function: inherit;

	pointer-events: none;
}

.textfield-input {
	display: block;

	line-height: inherit;

	border: none;
	border-bottom-width: 0.1em;
	border-bottom-style: solid;
	border-bottom-color: inherit;
	resize: none;
	font-size: 1em;
	padding-top: 0.5em;
	padding-bottom: 0.5em;
	margin: 0;
	outline: none;

	width: 100%;

	transition-property: border-bottom-width;
	transition-duration: inherit;
	transition-timing-function: inherit;
}

.textfield-helper {
	margin-top: 0.4em;
	font-size: 0.8em;
}

.textfield.isTouched {
	padding-top: 1em;
}

.textfield.isTouched .textfield-label {
	font-size: 0.8em;
	margin-top: -1em;
	height: auto;
}

.textfield.isTouched .textfield-input {
	border-bottom-width: 0.2em;
}

</style>
