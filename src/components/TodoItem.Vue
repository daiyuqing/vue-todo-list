<template>
	<div class="item_wrap"  v-bind:class="{ finished: todo.finished}"> 
		<input type="checkbox" v-model='todo.finished'>
		<input class="item_text" type="text" v-model='todo.text'>
		<p class="time">{{todo.addTime}}</p>
		<span @click='deleteItem(index)' class="delete_btn">删除</span>
	</div>
</template>
<script type="text/javascript">
	export default {
		name:'TodoItem',
		props:['todo','deleteItem','index'],
		created:function(){
			console.log(this._props)
		}
	}
</script>
<style type="text/css" scoped>
	.item_wrap{
		display: flex;
		height: 40px;
		width: 500px;
		align-items: center;
		justify-content: space-between;
		background: #fff;
		padding:0 10px;
		margin-bottom: 5px;
		border-radius: 5px;
	}
	.finished{
		background: #f5f5f5;
	}
	.item_text{
		width: 200px;
		border:none;
		background: transparent;
		text-overflow: ellipsis;
		cursor: pointer;
	}
	.item_time{
		width: 200px;
	}
	.delete_btn{
		cursor: pointer;
	}
</style>