<template>
	<view>
		<!-- 头部搜索栏 -->
		<view class="header">
			<view class="left-arrow">
				<text class="iconfont icon-arrow-left" 
				style="margin: auto; font-size: 62.5rpx;color: #666;">
				</text>
			</view>
			<uni-search-bar 
			:radius="20" 
			class="searchInputBar"
			cancelButton="none"
			/>
			<view class="searchText">
				<text>搜索</text>
			</view>
		</view>
		<!-- 热门搜索 -->
		<view>
			
		</view>
	</view>
</template>

<script>
	import uniSearchBar from '@/components/uni-search-bar/uni-search-bar.vue'
	export default {
		data() {
			return {
				
			}
		},
		components:{
			uniSearchBar
		}
	}
</script>

<style>
	.header{
		height: 104.16rpx;
		line-height: 104.16rpx;
		display: flex;
		justify-content: space-between;
		align-items: center;
	}
	.left-arrow{
		width: 116.66rpx;
		display: flex;
		justify-content: center;
	}
	.searchText{
		width: 93.75rpx;
		display: flex;
		justify-content: center;
		padding-right: 20.83rpx;
		font-size: 37.5rpx;
	}
	.searchInputBar{
		margin-right: 20.83rpx;
		flex-grow: 1;
	}
</style>
