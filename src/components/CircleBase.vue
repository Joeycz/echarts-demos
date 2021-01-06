<template>
	<div>
		<div>环形</div>
		<div class="box box1">
			<v-chart :options="circleData" :init-options="initOptions"></v-chart>
		</div>
		<div class="box box2">
			<v-chart :options="roundCircle" :init-options="initOptions"></v-chart>
		</div>
		<div class="box box3">
			<v-chart :options="lineData" :init-options="initOptions"></v-chart>
		</div>
		<div class="box box4">
			<v-chart :options="radarData" :init-options="initOptions"></v-chart>
		</div>
	</div>
</template>

<script>
import ECharts from 'vue-echarts'
import * as echarts from 'echarts/dist/echarts.js'
import 'echarts/lib/chart/pie'
import 'echarts/lib/component/legend'
import 'echarts/lib/chart/bar'
import 'echarts/lib/component/polar'
import 'echarts/lib/chart/line'
import 'echarts/lib/chart/radar'
console.log(echarts)
export default {
	name: 'CircleBase',
	components: {
		'v-chart': ECharts
	},
	props: {
		data: {
			type: Array,
			default: function() {
				return []
			}
		}
	},
	data() {
		return {
			initOptions: {
        renderer: 'canvas'
      },
			pieData: {
				title: {
					text: '饼图程序调用高亮示例',
					x: 'center'
				},
				tooltip: {
					trigger: 'item',
					formatter: '{a} <br/>{b} : {c} ({d}%)'
				},
				legend: {
					orient: 'vertical',
					left: 'left',
					data: ['直接访问', '邮件营销', '联盟广告', '视频广告', '搜索引擎']
				},
				series: [
					{
						name: '访问来源',
						type: 'pie',
						radius: '55%',
						center: ['50%', '60%'],
						data: [
							{ value: 335, name: '直接访问' },
							{ value: 310, name: '邮件营销' },
							{ value: 234, name: '联盟广告' },
							{ value: 135, name: '视频广告' },
							{ value: 1548, name: '搜索引擎' }
						],
						itemStyle: {
							emphasis: {
								shadowBlur: 10,
								shadowOffsetX: 0,
								shadowColor: 'rgba(0, 0, 0, 0.5)'
							}
						}
					}
				]
			},
			circleData: {
				animation : false,
				legend: {
					icon: 'circle',
					orient: 'horizontal',
					left: 0,
					data: ['直接访问', '邮件营销', '联盟广告', '视频广告', '搜索引擎'],
					textStyle: {
						fontSize: 10,
						color: 'blue'
					},
					itemWidth: 4,
					itemHeight: 4
				},
				series: [
						{
							name: '访问来源',
							type: 'pie',
							radius: ['30%', '70%'],
							avoidLabelOverlap: false,
							hoverAnimation: false,
							label: {
								show: false,
								position: 'center'
							},
							labelLine: {
								show: false
							},
							color: ['red', 'green', 'yellow', 'blueviolet'],
							data: [
								{value: 335, name: '直接访问'},
								{value: 310, name: '邮件营销'},
								{value: 234, name: '联盟广告'},
								{value: 135, name: '视频广告'},
								{value: 1548, name: '搜索引擎'}
							]
						}
				]
			},
			roundCircle: {
				animation: false,
				angleAxis: {
					max: 100, // 满分
					clockwise: true, // 逆时针
					// 隐藏刻度线
					axisLine: {
						show: false
					},
					axisTick: {
						show: false
					},
					axisLabel: {
						show: false
					},
					splitLine: {
						show: false
					}
				},
				radiusAxis: {
					type: 'category',
					// 隐藏刻度线
					axisLine: {
						show: false
					},
					axisTick: {
						show: false
					},
					axisLabel: {
						show: false
					},
					splitLine: {
						show: false
					}
				},
				polar: {
					center: ['50%', '50%'],
					radius: '280' // 图形大小
				},
				series: [
					{
						type: 'bar',
						data: [{
							name: '作文得分',
							value: 75,
							itemStyle: {
								normal: {
									color: '#aaf14f'
								}
							},
						}],
						coordinateSystem: 'polar',
						roundCap: true,
						barWidth: 20,
						barGap: '-100%', // 两环重叠
						z: 2,
					},
					{ // 灰色环
						type: 'bar',
						data: [{
							value: 100,
							itemStyle: {
								color: '#e2e2e2'
							}
						}],
						coordinateSystem: 'polar',
						roundCap: true,
						barWidth: 20,
						barGap: '-100%', // 两环重叠
						z: 1
					}
				]
			},
			lineData: {
				grid: {
					x: 50,
					y: 25,
					x2: 30,
					y2: 35
				},
				xAxis: {
					show: true,
					type: 'category',
					data: ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun'],
					spiltLine: {
						show: false
					}
				},
				yAxis: {
					type: 'value',
					show: true,
					spiltLine: {
						show: false
					}
				},
				series: [{
					symbol: 'none',
					data: [820, 932, 901, 934, 1290, 1330, 1320],
					type: 'line',
					smooth: true
				},{
					symbol: 'none',
					data: [82, 93, 901, 934, 120, 133, 130],
					type: 'line',
					smooth: true
				}]
			},
			radarData: {
				title: {
						text: '基础雷达图'
				},
				tooltip: {},
				legend: {
					left: 'left',
					data: ['预算分配', '实际开销']
				},
				radar: {
						// shape: 'circle',
						name: {
							show: false,
							textStyle: {
								color: '#fff',
								backgroundColor: '#999',
								borderRadius: 3,
								padding: [3, 5]
							}
						},
						indicator: [
								{ name: '销售（sales）', max: 6500},
								{ name: '管理（Administration）', max: 16000},
								{ name: '信息技术（Information Techology）', max: 30000}
						]
				},
				series: [{
						name: '预算 vs 开销（Budget vs spending）',
						type: 'radar',
						// areaStyle: {normal: {}},
						data: [
								{
									value: [4300, 10000, 28000],
									name: '预算分配'
								},
								{
									value: [5000, 14000, 28000],
									name: '实际开销'
								}
						]
				}]
			}
		}
	}
}
</script>

<style lang="less">
.echarts {
	width: 300px;
	height: 300px;
}
</style>

<style lang="less" scoped>
.box1 {
	background: skyblue;
}
.box2 {
	background: yellowgreen;
}
.box {
	display: inline-block;
	margin: 0 auto;
	border: 1px solid #dddddd;
}
.box + .box {
	margin-top: 10px;
	margin-left: 10px;
}
</style>