<template>
	<view class="cart-container">
		<!-- 收获地址组件 -->
		<my-address></my-address>
		<!-- 商品列表的标题区域 -->
		<view class="cart-title">
			<!-- 左侧图标 -->
			<uni-icons type="shop" size="18"></uni-icons>
			<!-- 右侧文本 -->
			<text class="cart-title-text"> 购物车</text>
			
		</view>
		<!-- 循环渲染购物车中的商品信息 -->
		
			
		
		
		<uni-swipe-action>
			<block v-for="(goods,i) in cart" :key="i">
			<uni-swipe-action-item :right-options="options" @click="swipeItemClickHandler(goods)">
				<my-goods :goods="goods" :show-radio="true" :show-num="true" @radio-change="radioChangeHandler" @num-change="numberChangeHandler"></my-goods>
			</uni-swipe-action-item>
			</block>
		</uni-swipe-action>
		
		<!-- 自定义结算组件 -->
		<my-settle></my-settle>
		
	</view>
</template>

<script>
	import badgeMix from '@/mixnis/tabbar-badge.js'
	import {mapState,mapMutations} from 'vuex'
	export default {
		mixins:[badgeMix],
		computed:{
			...mapState('m_cart',['cart'])
		},
		data() {
			return {
				options:[{
					text:'删除',
					style:{
						backgroundColor:'#c00000'
					}
				}]
			};
		},
		methods:{
			...mapMutations('m_cart',['updateGoodsState','updateGoodsCount','removeGoodsById']),
			radioChangeHandler(e){
				console.log(e)
			},
			numberChangeHandler(e){
				console.log(e)
			},
			swipeItemClickHandler(goods){
				this.removeGoodsById(goods.goods_id)
			}
		}
	
	}
</script>

<style lang="scss">
.cart-title{
	height: 40px;
	display: flex;
	align-items: center;
	padding-left: 5px;
	border-bottom: 1px solid #efefef;
	.cart-title-text{
		font-size: 14px;
		margin-left: 10px;
	}
}
.cart-container{
	padding-bottom: 50px;
}
</style>
