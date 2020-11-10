# xcw-number

## 属性说明

|属性名		|类型			|默认值	|说明							|
| -- 		| -- 			| --	|--								|
| value 	| Number 		| 1		| 输入框当前值 					|
| min 		| Number 		| 0 	| 最小值 						|
| max 		| Number 		| 100	| 最小值 						|
| step 		| Number	 	| 1		| 每次点击改变的间隔大小			|
| disabled 	| Boolean		| false	| 是否为禁用状态[true|false]		|
| width 	| Number		| 80	| 输入框的宽度					|
| size	 	| String		| mini	| mini small medium 小 中 大		|
| waive	 	| Boolean		| true	| 是否保留两位小数[true|false]	|

## 需要双向绑定
```html
	@input="e => value = e"
	value 为当前需要绑定的变量
```

## 使用示例

```html
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
```

```javascript
import xcwNumber from '@/components/xcw-number/xcw-number.vue'
export default {
	components:{
		xcwNumber
	},
	data(){
		return{
			
		}
	}
}
```
