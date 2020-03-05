<template>
	<view class="shop-item-container">
		<view class="shop-item-logo">
			<image class="shop-item-logo" mode="aspectFill" :src="shop.logo"></image>
		</view>
		<view class="shop-item-content">
			<view class="shop-item-content-top">
				<view class="shop-item-title single-line">{{shop.title}}</view>
				<view class="shop-item-description">{{'['+ (shop.location || "") +']' + shop.description}}</view>
			</view>
			<view class="shop-item-content-bottom">
				<view>
					<text class="shop-item-content-price">{{shop.price}}</text>
					<text class="shop-item-content-price-unit">元</text>
					<text>门市价:{{shop.originPrice}}元</text>
				</view>
				<view class="shop-item-content-sold">
					<text>已售:{{shop.sold}}</text>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		name: 'ShopItem',
		props: {
			shop: Object
		},
		data() {
			return {
				
			}
		}
	}
</script>

<style>
	.shop-item-container{
		display: flex;
		align-items: center;
		padding: 32.31rpx 0;
		height: 207.7rpx;
		border-bottom: 1px solid #DDD8CE;
	}
	.shop-item-logo{
		width: 207.7rpx;
		height: 207.7rpx;
	}
	.shop-item-content{
		display: flex;
		flex-direction: column;
		justify-content: space-between;
		height: 207.7rpx;
		margin-left: 23.07rpx;
	}
	.shop-item-title{
		padding-top: 13.84rpx;
		font-size: 34.61rpx;
		font-weight: 400;
		margin-bottom: 16.61rpx;
		width: 473.11rpx;
	}
	.shop-item-description{
		color: #666;
		font-size: 27.69rpx;
		width: 484.65rpx;
	}
	.shop-item-content-bottom{
		display: flex;
		justify-content: space-between;
		font-size: 27.69rpx;
		color: #666;
	}
	.shop-item-content-price{
		font-size: 41.54rpx;
		color: #F60;
	}
	.shop-item-content-price-unit{
		color: #F60;
		margin-right: 11.53rpx;
	}
	.shop-item-content-sold{
		height: 46.15rpx;
		line-height: 46.15rpx;
		margin-top: 5.76rpx;
		margin-right: 10.41rpx;
	}
</style>
