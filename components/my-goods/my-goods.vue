<template>
	<view class="goods-item">
		<!-- 左侧的盒子 -->
		<view class="goods-item-left">
			<radio :checked="goods.goods_state" color="#c00000" v-if="showRadio" @click="radioClickHandler"></radio>
			<image :src="goods.goods_small_logo || defaultPic" class="goods-pic"></image>
		</view>
		<!-- 右侧盒子 -->
		<view class="goods-item-right">
			<view class="goods-name">{{goods.goods_name}}</view>
			<view class="goods-info-box">
				<view class="goods-price">￥{{goods.goods_price |tofixed}}</view>
				<uni-number-box :min="1" :value="goods.goods_count" v-if="showNum" @change="numChangeHandler"></uni-number-box>
					
				
				
			</view>
			
		</view>
	</view>
</template>

<script>
	export default {
		props:{
			goods:{
				type:Object,
				default:{}
			},
			showRadio:{
				type:Boolean,
				default:false
			},
			showNum:{
				type:Boolean,
				default:false
			}
		},
		
		data() {
			return {
				//默认图片
				defaultPic:'https://image.baidu.com/search/detail?ct=503316480&z=0&ipn=d&word=%E5%9B%BE%E7%89%87%E4%B8%8D%E5%AD%98%E5%9C%A8&step_word=&hs=0&pn=2&spn=0&di=7264239678495129601&pi=0&rn=1&tn=baiduimagedetail&is=0%2C0&istype=0&ie=utf-8&oe=utf-8&in=&cl=2&lm=-1&st=undefined&cs=1351874568%2C1174672055&os=3073145961%2C2652048664&simid=3266037534%2C259859904&adpicid=0&lpn=0&ln=1851&fr=&fmq=1700925651651_R&fm=&ic=undefined&s=undefined&hd=undefined&latest=undefined&copyright=undefined&se=&sme=&tab=0&width=undefined&height=undefined&face=undefined&ist=&jit=&cg=&bdtype=0&oriquery=&objurl=https%3A%2F%2Fstatic.sensorexpert.com.cn%2Fcaiji%2Fc2a0948024080c76068c2bcd8dcb1366%2F20220427%2F6371b371-b3ca-41f1-9309-99c51089ac94.png&fromurl=ippr_z2C%24qAzdH3FAzdH3Fooo_z%26e3Bfjgf56jxrj6p_z%26e3Bv54_z%26e3BvgAzdH3Fw6ptvsjAzdH3F999bl_z%26e3Bip4s&gsm=1e&rpstart=0&rpnum=0&islist=&querylist=&nojc=undefined&dyTabStr=MCwzLDEsMiw0LDYsNSw3LDgsOQ%3D%3D&lid=10764914853927254411'
			};
		},
		filters:{
			tofixed(num){
				return Number(num).toFixed(2)
			}
		},
		methods:{
			//这是radio组件的点击事件的处理函数
			radioClickHandler(){
				this.$emit('radio-change',{
					goods_id:this.goods.goods_id,
					goods_state:!this.goods.goods_state
				})
			},
			//监听到了numberbox组件数量变化的组件
			numChangeHandler(val){
				console.log(val)
				this.$emit('num-change',{
					goods_id:this.goods.goods_id,
					goods_count:+val
				})
			}
		}
	}
</script>

<style lang="scss">
.goods-item{
	display: flex;
	padding: 10px 5px;
	border-bottom: 1px solid #f0f0f0;
	width: 750rpx;
	box-sizing: border-box;
	.goods-item-left{
		margin-left: 5px;
		display: flex;
		justify-content: space-between;
		align-items: center;
		.goods-pic{
			width: 100px;
			height: 100px;
			display: block;
		}
	}
	.goods-item-right{
		display: flex;
		flex: 1;
		flex-direction: column;
		justify-content: space-between;
		.goods-name{
			
			font-size: 13px;
		}
		.goods-info-box{
			display: flex;
			justify-content: space-between;
			align-items: center;
			
		}
		.goods-price{
			color: #c00000;
			font-size: 16px;
		}
	}
}
</style>