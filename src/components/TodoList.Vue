<template>
	<div>
		<input 
			type="text" 
			v-model='inputText'
			@keyup.enter="submit"
			placeholder="添加待办项" 
		>
		<div class="title">
			<p>正在进行</p>
			<span>{{todoNum}}</span>
		</div>
		<transition-group name="list" tag="p">
			<TodoItem 
				v-for='(todo,index) in todos'
				v-if='!todo.finished'
				:todo='todo'
				:index='index'
				:key='todo.id'
				:deleteItem='deleteItem'
			></TodoItem>
		</transition-group>
		<div class="title">
			<p>已经完成</p>
			<span>{{finishedNum}}</span>
		</div>
		<transition-group name="list" tag="p">
			<TodoItem 
				v-for='(todo,index) in todos'
				v-if='todo.finished'
				:todo='todo'
				:index='index'
				:key='todo.id'
				:deleteItem='deleteItem'
			></TodoItem>
		</transition-group>	
	</div>
</template>
<script type="text/javascript">
	import TodoItem from '@/components/TodoItem'
	export default {
		name:'TodoList',
		components:{TodoItem},
		data: function() {
			return{
				inputText: '',
				todos:[],
				id:1,
			}
		},
		computed:{
			todoNum:function(){
				let todoNum=0;
				for(let i in this.todos){
					if (this.todos[i].finished==false) {
						todoNum++;
					}
				}
				return todoNum;
			},
			finishedNum:function(){
				let finishedNum=0;
				for(let i in this.todos){
					if (this.todos[i].finished) {
						finishedNum++;
					}
				}
				return finishedNum;
			},
		},
		methods:{
			submit:function(){
				if (this.inputText!='') {
					this.todos.push({id:this.id,text:this.inputText,addTime:new Date().toLocaleString(),finished:false});
					this.inputText='';
					this.id++;
				}
			},
			deleteItem:function(index){
				this.todos.splice(index,1);
			}
		}
	}
</script>
<style type="text/css" scoped>
	*{
		margin: 0;
		padding:0;
	}
	div{
		margin: 0 auto;
	}
	input{
		width: 400px;
		height: 25px;
		border-radius: 25px;
		-web-kit-appearance:none;
		-moz-appearance: none;
		border:1px solid #c8cccf;
		color:#6a6f77;
		outline:0;
		padding-left: 15px;
	}
	
	.title{
		width: 500px;
		display: flex;
		align-items: center;
		justify-content: space-between;
		margin-top: 20px;
		margin-bottom: 20px;
	}
	.title p{
		font-size: 25px;
	}
	.title span{
		font-size: 18px;
		display: inline-block;
		width: 25px;
		height: 25px;
		line-height: 25px;
		border-radius: 25px;
		background: #ccc;
	}
	.list-item {
	    display: inline-block;
	    margin-right: 10px;
	}
	.list-enter-active, .list-leave-active {
	    transition: all 1s;
	}
	.list-enter, .list-leave-to
	/* .list-leave-active for below version 2.1.8 */ {
	    opacity: 0;
	    transform: translateX(30px);
	}
</style>