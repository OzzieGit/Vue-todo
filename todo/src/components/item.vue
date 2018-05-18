<template>
	<div>
		<label @click='checked'>
			<input type="checkbox" v-model="item.status" />
			<span :class='{ end : item.status }'>{{ item.content }}</span>
		</label>
		<b @click='delItem'>X</b>
	</div>
</template>

<script>
	export default {
		props:{
			item:{
				type:Object,
				required:true
			}
		},
		methods:{
			delItem:function(){
				this.$emit('del',this.item.id)
			},
			checked(){
				this.$emit('checked',this.item.id)
			}
		}
	}
</script>

<style scoped>
div{ line-height: 46px; padding: 0 0 0 20px; background-color: rgba(255,255,255,0.5); border-bottom: 1px solid #ddd; }
div label span{ display: inline-block; line-height: 46px; color: #666; user-select: none; cursor: pointer; }
div label span.end{ text-decoration: line-through; }
div input{ float: left; width: 30px; height: 46px; border: none ; outline: none ; appearance: none; cursor: pointer; background: url(../assets/round.png) no-repeat center left; background-size: 20px 20px; opacity: 0.7; }
div input:checked{ background: url(../assets/done.png) no-repeat center left; background-size: 20px 20px; }
div b{ float: right; width: 46px; height: 46px; line-height: 46px; text-align: center; cursor: pointer; color: #999; font-weight: 100; }
</style>
