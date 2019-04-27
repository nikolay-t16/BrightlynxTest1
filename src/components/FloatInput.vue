<template>
	<input v-model=value type="text" v-on:keydown="onKeydown"/>
</template>

<script>
	export default {
		name: "FloatInput",
		props: ['value'],
		data: function () {
			return {}
		},
		methods: {
			onKeydown: function (e) {
				if (!isNaN(e.key))
					return;
				if (e.key == "." && this.value.indexOf(".") ===  -1) {
					return;
				}
				e.preventDefault();
			}
		}
	}
</script>

<style scoped>

</style>