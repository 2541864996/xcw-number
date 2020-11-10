<template>
	<view class="main" :style="'width:'+(minusWidth+inputWidth+plusWidth)+'rpx;height:'+height+'rpx;'">
		<view class="boder" >
			<view @click="changeValue('minus')" class="minus" :style="'width:'+minusWidth+'rpx;font-size:'+fontSize+'rpx'"
				:class="{'disabled': inputValue <= min || disabled }">
				-
			</view>
			
			<input :disabled="disabled" @blur="onBlur" type="number" v-model="inputValue" class="interior value-font" 
				   :style="'width:'+inputWidth+'rpx;margin-left:'+ minusWidth +'rpx;font-size:'+(fontSize-10)+'rpx'"
				   :class="{ 'disabled': disabled }"/>
					
			<view @click="changeValue('plus')" class="plus" :style="'width:'+plusWidth+'rpx;font-size:'+fontSize+'rpx'"
				:class="{ 'disabled': inputValue >= max || disabled }">
				+
			</view>
		</view>
	</view>
</template>

<script>
	/**
	 * xcw-Number 计步器
	 * @description 计步器
	 * @tutorial https://ext.dcloud.net.cn/plugin?id=31
	 * @property {Number} value 输入框当前值
	 * @property {Number} min 最小值
	 * @property {Number} max 最大值
	 * @property {Number} step 每次点击改变的间隔大小
	 * @property {Boolean} disabled = [true|false] 是否为禁用状态
	 * @property {Numver} width 输入框的宽度
	 * @property {String} size = mini small medium 小 中 大
	 * @property {Boolean} waive = [true|false] 是否保留两位小数
	 * @event {Function} changeValue 改变值 minus减 plus加
	 * @event {Function} onBlur 输入事件
	 * @event {Function} sizeVerify 验证大小是否超出限制
	 */
	export default {
		name: "number",
		props: {
			value: {
				type: [Number, String],
				default: 1
			},
			min: {
				type: Number,
				default: 0
			},
			max: {
				type: Number,
				default: 100
			},
			step: {
				type: Number,
				default: 1
			},
			disabled: {
				type: Boolean,
				default: false
			},
			width:{
				type: Number,
				default: 80
			},
			size:{
				type:String,
				default:"mini"
			},
			waive:{
				type:Boolean,
				default: true
			}
		},
		created(){
			this.inputValue = +this.value;
			let heigth = 50;
			let fontSize = 35;
			this.inputWidth = this.width; 
			switch(this.size){
				case 'mini':
					height = 50;
					fontSize = 35;
					break;
				case 'small':
					heigth = 80;
					fontSize = 50;
					break;
				case 'medium':
					heigth = 110;
					fontSize = 70;
					this.inputWidth = 150;
					break;
				default:
					heigth = 50;
					fontSize = 35;
					break;
			}
			this.height = heigth;
			this.plusWidth = heigth;
			this.minusWidth = heigth;
			this.fontSize = fontSize;
			
		},
		data() {
			return {
				inputValue: 0,
				plusWidth:50,
				minusWidth:50,
				height:50,
				fontSize:35,
				inputWidth:80,
			};
		},
		watch: {
			inputValue(newVal, oldVal) {
				if (newVal !== oldVal) {
					this.$emit('input', this.inputValue);
				}
			}
		},
		methods: {
			/* 改变值 */
			changeValue(type) {
				if (this.disabled) {
					return;
				}
				let number = this.inputValue;
				if(type === "plus"){
					number += this.step;
				}else if(type === "minus"){
					number -= this.step;
				}
				this.digitVerify(number);
				this.sizeVerify(number);
			},
			/**
			 * 输入框事件
			 * @param {Object} event.detail.value 当前输入的值
			 * @explain 如果没有输入值则修改当前值为默认最小值
			 * 			
			 */
			onBlur(event) {
				let value = event.detail.value;
				if (!value) {
					this.inputValue = this.min;
					return;
				}
				this.digitVerify(parseFloat(value));
				this.sizeVerify(parseFloat(value));
			},
			/**
			 * 验证数字是否超出大小限制
			 * @param {Object} number 验证的数字
			 * @explain 超过最大值设置为最大值 低于最小值设置为最小值
			 */
			sizeVerify(number){
				if(number < this.min){
					this.inputValue = this.min;
				}else if(number > this.max){
					this.inputValue = this.max;
				}
			},
			/**
			 * 小数验证
			 * @param {Object} number 验证的数字
			 * @explain 开启小数保留两位则进行四舍五入
			 */
			digitVerify(number){
				//小数处理
				if(this.waive){
					number = Math.floor(number * 100) / 100; 
				}
				this.inputValue = number;
			},
		}
	};
</script>

<style>
	.main{
		display: block; 
		margin: 5px;
	}
	.minus{
		position: absolute;
		left: 0;
		height:100%;
		border-right: 1px solid #dcdfe6;
		height: 100%;
		text-align: center;
		vertical-align:middle;
	}
	.plus{
		position: absolute;
		right: 0;
		height:100%;
		overflow: hidden;
		display:inline-block;
		border-left: 1px solid #dcdfe6;
		text-align: center;
		height: 100%;
		vertical-align:middle;
	}
	.interior{
		height:100%;
		display:inline-block;
		text-align: center;
		height: 100%;
		vertical-align:middle;
	}
	.boder{
		border-radius: 4px;
		border: 1px solid #dcdfe6;
		height: 100%;
		position:relative;
	}
	.value-font{
		font-size:25rpx;
		font-family:"微软雅黑","黑体","宋体";
	}
	input{
		overflow: inherit;
	}
	.disabled {
		color: #c0c0c0;
	}
</style>
