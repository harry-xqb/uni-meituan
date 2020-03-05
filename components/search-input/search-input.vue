<template>
	<view class="search-input">
		<text 
		class="iconfont icon-search"
		 style="height: 66.66rpx; line-height: 66.66rpx; font-size: 37.5rpx;"
		 >
		 </text>
		<input class="input"  placeholder="请输入商家名丶品类或商圈..." maxlength="-1" @focus="onSearchFocus"/>
	</view>
</template>

<script>
	export default{
		name: "SearchInput",
		methods:{
			onSearchFocus(){
				this.$emit("onFocus")
			}
		},
		data(){
			return{
				
			}
		}
	}
</script>

<style>
	.search-input{
		height: 104.16rpx;
		width: 469.04rpx;
		height: 66.66rpx;
		margin-right: 20rpx;
		background-color: #FFF9E5;
		border-radius: 20rpx;
		padding-left: 20rpx;
		display: flex;
	}
	.input{
		height: 66.66rpx;
		line-height: 66.66rpx;
	}
</style>
