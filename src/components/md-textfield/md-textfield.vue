<template>
	<div>
		<div class="textfield" :class="{ isTouched: focus || hasText() }">
			<div class="textfield-label" :class="accentForeground">{{ label }}</div>
			<textarea :rows="rowCount()" class="textfield-input" v-model="text" @focus="focus = true" @blur="focus = false" @input="cleanText()"></textarea>
			<div class="textfield-line" :class="accentBackground"></div>
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
		multiline: { default: false },
		accent: { default: 'primary' }
	},
	data() {
		return {
			text: 'touched',
			focus: false,
			accentForeground: '',
			accentBackground: ''
		}
	},
	mounted() {
		this.setAccent();
	},
	watch: {
		focus: function() {
			this.setAccent();
		}
	},
	methods: {
		setAccent() {
			let accent = (this.focus ? this.accent : 'default');
			accent = accent == 'default' ? 'dark' : accent;

			this.accentBackground = [ 'background--'+accent ];
			this.accentForeground = [ 'foreground--'+accent ];
		},

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

	padding-top: 1em;
	padding-bottom: 0.5em;
}

.textfield-label {
	top: 1.5em;
	padding-left: 0.12em;
	line-height: inherit;

	position: absolute;
	transition-property: font-size,margin-top,color;
	transition-duration: inherit;
	transition-timing-function: inherit;

	pointer-events: none;
}

.textfield-input {
	display: block;

	font-family: inherit;
	line-height: inherit;

	border: none;

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

.textfield-line {
	position: absolute;
	width: 100%;

	transition-property: height,background-color;
	transition-duration: inherit;
	transition-timing-function: inherit;
	height: 1px;
}

.textfield.isTouched .textfield-line {
	height: 2px;
}

.textfield-helper {
	margin-top: 0.5em;
	font-size: 0.8em;
}

.textfield.isTouched .textfield-label {
	font-size: 0.8em;
	margin-top: -1.2em;
	height: auto;
}

</style>
