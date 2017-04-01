<template>
	<div class="icon" :class="'icon--'+size">{{ name }}</div>
</template>

<script>
export default {
	props: {
		name: { required: true },
		size: { default: 'small' }
	}
}
</script>


<style>
@import url('https://fonts.googleapis.com/icon?family=Material+Icons');

.icon {
	font-family: 'Material Icons';
	font-weight: normal;
	font-style: normal;
	display: inline-block;
	line-height: 1;
	text-transform: none;
	letter-spacing: normal;
	word-wrap: normal;
	white-space: nowrap;
	direction: ltr;
	vertical-align: sub;
}

.icon--small { /* 18 */
	font-size: 1.2em;
}

.icon--medium { /* 24 */
	font-size: 1.5em;
}

.icon--large { /* 36 */
	font-size: 2.3em;
}

.icon--larger { /* 48 */
	font-size: 3em;
}
</style>
