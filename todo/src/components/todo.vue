<template>
	<div id="todo">
		<div class="ipt">
			<input type="text" autofocus="true" placeholder="接下来要做什么" v-model="text" />
			<input type="button" value="添加" @click="addItem" />
		</div>
		<item v-for="item in filterList" :key="item.id" :item="item" @del="delItem" @checked="checked"></item>
		<div v-if="filterList.length == 0" class="not">列表为空</div>
		<tabs :list='filterList' :filter="filter" @delList="delAll" @toggleTodo='toggle'></tabs>
	</div>
</template>

<script>
	import Item from './item'
	import Tabs from './tabs'
	export default {
		name: 'todo',
		data(){
			return {
				id:0,
				text:'',
				todoList:[],
				filter:'all'
			}
		},
		computed:{
			filterList(){
				if(this.filter === 'all'){
					return this.todoList
				}else if(this.filter === 'complete'){
					return this.todoList.filter(item => item.status == true)
				}else if(this.filter === 'imperfectly'){
					return this.todoList.filter(item => item.status == false)
				}
			}
		},
		methods:{
			addItem(){
				if(this.text == ''){ return }
					this.todoList.unshift({
						id:++this.id,
						content:this.text.trim(),
						status:false
					})
				this.text = '';
				this.localStorageSetItem()
			},
			delItem(id){
				this.todoList = this.todoList.filter(item=> item.id != id );
				this.localStorageSetItem()
			},
			checked(id){
				this.todoList.forEach(i=>{
					if(i.id == id){
						i.status = !i.status
					}
				})
				this.localStorageSetItem()
			},
			delAll(){
				if(this.filter === 'all'){
					this.todoList = [];
				}else if(this.filter === 'complete'){
					this.todoList = this.todoList.filter(item => item.status != true)
				}else if(this.filter === 'imperfectly'){
					this.todoList = this.todoList.filter(item => item.status != false)
				}
				this.localStorageSetItem()
			},
			toggle(filter){
				this.filter = filter;
			},
			localStorageSetItem(){
				localStorage.clear();
				localStorage.setItem("todoList", JSON.stringify(this.todoList));
			}
		},
		created(){
			this.todoList = JSON.parse(localStorage.getItem("todoList")) || [];
			this.id = this.todoList.length == 0 ? 0 : this.todoList[0].id;
		},
		components:{
			Item,
			Tabs
		}
	}
</script>

<style scoped>
#todo{ width: 500px; margin: 20px auto 50px; }
#todo .ipt{ height: 46px; }
#todo .ipt input{ height: 46px; line-height: 46px; font-size: 16px; border: none; color: #666; }
#todo .ipt input[type='text']{ width: 80%; float: left; text-indent: 20px;  }
#todo .ipt input[type='button']{ width: 20%; float: right; cursor: pointer; }
.not{ line-height: 46px; text-align: center; background-color: rgba(255,255,255,0.7); color: rgba(175,47,47,0.7); }
</style>
