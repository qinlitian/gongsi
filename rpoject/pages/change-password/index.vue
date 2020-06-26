<template>
	<view class="content">
		<view class="c-top">
			<text class="t">会员账号管理</text>
			<button class="but"
			>修改密码</button>
		</view>
		
		<view class="c-list"
		style="width: 100%;"
		v-for="(item,index) in list"
		:key='item'
		>
		<label>
			<checkbox :value="index + ''" />
			<text>{{ item }}</text>
		</label>
		
		<view class="change-remove">
			<button type="default"
			@click="modify"
			>modify</button>
			<button type="default"
			@click="remove"
			style="float: right;"
			>remove</button>
		</view>
		
		</view>
			<button class="add-accound">添加新账号</button>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				list:[1,2,3,4,5,6]
			};
		},
		methods:{
			modify(){
				uni.showModal({
					content:'是否要修改',
					success: function (res) {
						if (res.confirm) {
							console.log('用户点击确定修改');
						} else if (res.cancel) {
							console.log('用户点击取消修改');
						}
					}
				})
			},
			remove(){
				uni.showModal({
					content:'确定要删除吗',
					success: function (res) {
						if (res.confirm) {
							console.log('用户点击确定删除');
						} else if (res.cancel) {
							console.log('用户点击取消删除');
						}
					}
				})
			}
		}
	}
</script>

<style lang="scss" scoped>
	.content{
		width: 100%;
		height: 1000rpx;
		background-color: pink;
		.c-top{
			background-color: #dcdcdc;
			display: flex;
			justify-content: center;
			align-items: center;
			height: 70rpx;
			position: relative;
			.t{
				font-size: 35rpx;
				}
			.but{
				position: absolute;
				top: 0;
				right: 0;
				height: 70rpx;
				line-height: 70rpx;
				color: blue;
				background-color: #dcdcdc;
				}
			}
	}
		.c-list{
			border-bottom: 1rpx dashed #0000FF;
			padding-bottom: 5rpx;
		}
			.add-accound{
				width: 400rpx;
				height: 50rpx;
				margin-top: 40rpx;
				line-height: 50rpx;
				color: #FFFFFF;
				background-color: blue;
			}
			.change-remove{
				width: 300rpx;
				height: 55rpx;
				background-color: #000000;
				float: right;
				button{
					width: 40%;
					float: left;
					height: 50rpx;
					line-height: 50rpx;
				}
			}
	uni-button:after{
		border: none;
	}
</style>
