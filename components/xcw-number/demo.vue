<!-- xcw 计数器 -->
<template>
	<view>
		<view class="font-key">基础用法：</view>
		<xcw-number></xcw-number>
		
		<view class="font-key">禁用状态：</view>
		<xcw-number :disabled="true"></xcw-number>
		
		<view class="font-key">绑定值：</view>
		<xcw-number :value="value" @input="e => value = e"></xcw-number>
		{{value}}
		
		<view class="font-key">最小值：</view>
		<xcw-number :min="0"></xcw-number>
		<xcw-number :min="-1"></xcw-number>
		
		<view class="font-key">最大值：</view>
		<xcw-number :max="10"></xcw-number>
		<xcw-number :max="100"></xcw-number>
		
		<view class="font-key">步数：</view>
		<xcw-number :step="1"></xcw-number>
		<xcw-number :step="0.1"></xcw-number>
		
		<view class="font-key">宽度：</view>
		<xcw-number :width="100"></xcw-number>
		<xcw-number :width="120"></xcw-number>
		
		<view class="font-key">大小：</view>
		<xcw-number size="mini"></xcw-number>
		<xcw-number size="small"></xcw-number>
		<xcw-number size="medium"></xcw-number>
		
		<view class="font-key">是否保留两位小数：</view>
		<xcw-number :waive="false"></xcw-number>
		<xcw-number></xcw-number>
	</view>
</template>

<script>
	import xcwNumber from '@/my_components/xcw-number/xcw-number.vue';
	export default {
		name:"demo",
		components:{
			xcwNumber
		},
		data(){
			return{
				value:10,
			}
		}
	}
</script>

<style>
	.font-key{
		font-size: 32rpx;
		flood-color: #0066FF;
	}
</style>
