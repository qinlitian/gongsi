<template>
	<view class="qiun-columns">
		<view class="qiun-bg-white qiun-title-bar qiun-common-mt" >
			<!-- 顶部 title -->
			<!-- <view class="qiun-title-dot-light">柱状图旋转</view> -->
		</view>
		<view class="qiun-charts-rotate" >
			<canvas canvas-id="canvasColumn" id="canvasColumn" 
			class="charts-rotate" @touchstart="touchColumn"></canvas>
		</view>
		<button class="but"
		@click="tiao"
		>改密码</button>
	</view>
</template>

<script>
	import uCharts from '../../js_sdk/u-charts/u-charts/u-charts.js';
	var _self;
	var canvaColumn=null;
	export default {
		data() {
			return {
				cWidth2:'',//横屏图表
				cHeight2:'',//横屏图表
				pixelRatio:1,
			}
		},
		onLoad() {
			_self = this;
			this.cWidth2=uni.upx2px(700);
			this.cHeight2=uni.upx2px(1100);
			this.getServerData();
		},
		methods: {
			tiao(){
				uni.navigateTo({
					url:'../change-password/index'
				})
				},
			getServerData(){
				uni.request({
					url: 'https://www.ucharts.cn/data.json',
					data:{
					},
					success: function(res) {
						console.log(res.data.data)
						let ColumnColumn={categories:[],series:[]};
						//这里我后台返回的是数组，所以用等于，如果您后台返回的是单条数据，需要push进去
						ColumnColumn.categories=res.data.data.ColumnB.categories;
						ColumnColumn.series=res.data.data.ColumnB.series;
						_self.showColumnColumn("canvasColumn",ColumnColumn);
					},
					fail: () => {
						_self.tips="网络错误，小程序端请检查合法域名";
					},
				});
			},
			showColumnColumn(canvasId,chartData){
				canvaColumn=new uCharts({
					$this:_self,
					canvasId: canvasId,
					type: 'column',
					legend:{show:true},
					fontSize:15,
					background:'#FFFFFF',
					pixelRatio:_self.pixelRatio,
					animation: true,
					rotate:true,
					// #ifdef MP-ALIPAY || MP-BAIDU
					rotateLock:true,//百度及支付宝需要锁定旋转
					// #endif
					categories: chartData.categories,
					series: chartData.series,
					xAxis: {
						disableGrid:true,
					},
					yAxis: {
					
						disabled:true
					},
					dataLabel: true,
					width: _self.cWidth2*_self.pixelRatio,
					height: _self.cHeight2*_self.pixelRatio,
					extra: {
						column: {
							type:'group',
							width: _self.cWidth*_self.pixelRatio*0.45/chartData.categories.length,
							meter:{
								//这个是外层边框的宽度
								border:10,
								//这个是内部填充颜色
								fillColor:'#E5FDC3'
							}
						}
					  }
				});
				
			},
			touchColumn(e){
				canvaColumn.showToolTip(e, {
					format: function (item, category) {
						return category + ' ' + item.name + ':' + item.data 
					}
				});
			}
		}
	}
</script>

<style>
	.but{
		background-color: pink;
	}
	/*样式的width和height一定要与定义的cWidth和cHeight相对应*/
	.qiun-charts-rotate {
		width: 700upx;
		height: 1100upx;
		background-color: blue;
		padding: 25upx;
	}
	
	.charts-rotate {
		width: 700upx;
		height: 1100upx;
		background-color: #fff;
	}
</style>
