<template>
	<uni-list>
		<uni-list-item 
		:showArrow="false" 
		style="padding: 0;" 
		v-for="(item) in list" :key="item.id" :data-shopId="item.id"
		@tap="onShopItemTap(item.id)"
		>
			<shop-item :shop="item"/> 
		</uni-list-item>
	</uni-list>
</template>

<script>
	import uniList from "@/components/uni-list/uni-list/uni-list.vue";
	import uniListItem from "@/components/uni-list/uni-list-item/uni-list-item.vue";
	import shopItem from "@/components/shop-item/shop-item.vue";
	export default {
		name: "shop-list",
		props: {
			list: Array
		},
		components:{
			uniList,
			uniListItem,
			shopItem
		},
		methods: {
			onShopItemTap(shopId) {
				this.$emit("onShopItemTab", shopId);
			}
		}
	}
</script>
<style>
</style>
