<template>
	<svg>
		<use xlinkHref={"#" + props.name}></use>
	</svg>
</template>

<script lang="ts">
import type { PropType } from 'vue';
	export type IconName = 
	 "add"
	| "logo"
	| "left"
	| "more";
	export default {
		props:{
			name:{
				type: String as PropType<IconName>,
				required: true
			},
			onclick:{
				type: Function as PropType<(e:MouseEvent) => void>,
			}
		}
	}
</script>

<style lang="scss" scoped>

</style>
