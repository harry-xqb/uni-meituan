<template>
	<view class="page">
		<!-- 顶部导航 -->
		<view class="header">
			<view class="flex-horizontal-align-center" style="width: 140.71rpx; height: 100%;">
				<text class="location">
					<text style="padding-right: 9.38rpx;">杭州</text>
					<text class="iconfont icon-arrow-down" style="font-size: 28.14rpx;"></text>
				</text>
			</view>
			<view>
				<!-- <uni-search-bar cancelButton="none" bgColor="#FFF9E5"/> -->
				<search-input @onFocus="onSearchFocus"/>
			</view>
			<!-- <input class="search-input iconfont icon-search" placeholder="请输入商家名丶品类或商圈..." maxlength="-1" @focus="onSearchFocus"/> -->
			<view class="flex-horizontal-align-center" style="width: 88.18rpx; height: 100%;">
				<text class="iconfont icon-person" style="color:#333333; font-weight: bold; font-size: 36.92rpx;"/>
			</view>
		</view>
		<!-- 分类列表 -->
		<view class="category-container">
			<swiper class="swiper"
			 indicator-dots="true" 
			 indicator-color="white" 
			 indicator-active-color="#FE8C00"
			 >
				<swiper-item v-for="(page,pageIndex) in categoryList.length" :key="pageIndex">
					<view class="swiper-item">
						<view class="category-row">
							<category-icon 
								 v-for="item in categoryList[pageIndex]"
								:key="item.id"
								:icon="item.icon" 
								:background="item.background" 
								:description="item.description"/> 
						</view>
					</view>
				</swiper-item>
			</swiper>
		</view>
	
		<!-- 猜你喜欢 -->
		<view class="guess-user-like-container">
			<view style="padding: 18.76rpx 0; border-bottom: 1px solid #DDD8CE;">
				<text style="font-size: 39.23rpx">猜你喜欢</text>
			</view>
			<shop-list :list="shopList" @onShopItemTab="onShopItemTab"/>
		</view>
	</view>
</template>

<script>
	import shopList from "@/components/shop-list/shop-list.vue";
	import categoryIcon from "@/components/category-icon/category-icon.vue";
	import searchInput from "@/components/search-input/search-input.vue";
	import uni_request from '@/common/uni_request.js';
	import uniSearchBar from '@/components/uni-search-bar/uni-search-bar.vue'
	const request = uni_request({ // 有效配置项只有三个
	    baseURL: 'http://mock.wxseller.club/mock/5e54c50d2b27d4001662eb35/meituan', //baseURL
	    timeout: 3000, // 超时时间
	})
	export default { 
		data() {
			return {
				shopList: [],
				categoryList: [],
			}
		},
		onLoad() {
			uni.showLoading({
				title: "数据加载中"
			})
			const arr = [];
			arr.push(this.categoryListRequest())
			arr.push(this.guessLikeShopListRequest())
			Promise.all(arr).then((res) => {
				uni.hideLoading();
			})
			
		},
		methods: {
			onShopItemTab(shopId){ // 店铺条目被点击
				console.log("父组件接收到店铺id:" + shopId)
			},
			onSearchFocus(){ // 收缩输入框被focus
				uni.navigateTo({
					url: "../search/search"
				})
			},
			categoryListRequest(){ // 分类列表加载
				return request.get("/categoryList").then(res => {
					if(res.code == 0){
						const tmp = [];
						const pageNumber = res.data.length % 10 == 0 ? 
											  parseInt(res.data.length / 10) : parseInt(res.data.length / 10) + 1;
						for(let i = 0; i < pageNumber; i++){
							tmp.push(res.data.slice(i * 10, i * 10 + 10));
						}
						this.categoryList = tmp;
					}else{
						uni.showToast({
							title: json.msg
						})
					}
				}).catch(e => console.error(e));
			},
			guessLikeShopListRequest() { // 猜你喜欢列表加载
				return request.get("/guessLike/shopList").then(res => {
					if(res.code == 0){
						this.shopList = res.data;
					}else{
						uni.showToast({
							title: json.msg
						})
					}
				}).catch(e => console.error(e));
			}
		},
		components: {
			shopList,
			categoryIcon,
			searchInput,
			uniSearchBar
		}
	}
</script>
	
<style>
	.header{
		display: flex;
		flex-direction: row;
		align-items: center;
		background-image: linear-gradient(135deg, #FFD000 0%, #FFBD00 100%);
		height: 115.39rpx;
		line-height: 73.85rpx;
		padding-left: 20.83rpx;
	}
	.location{
		display: inline-block;
		vertical-align: middle;
		text-align: center;
		font-family: PingFangSC-Medium;
		font-size: 15px;
		color: #222222;
		height: 26px;
		line-height: 26px;
		margin-right: 20rpx;
	}
	.category-container{
		background-color: white;
		padding-bottom: 11.53rpx;
		border-bottom: 1px solid #DDD8CE;
	}
	.category-row{
		display: flex;
		flex-wrap: wrap;
	}
	.swiper {
		height: 415.41rpx;
	}
	.swiper-item {
		display: block;
		height: 415.41rpx;
		text-align: center;
	}
	.guess-user-like-container{
		background-color: white;
		margin-top: 23.07rpx;
		border-top: 1px solid #DDD8CE;
		padding: 23.07rpx
	}
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
	}
</style>
