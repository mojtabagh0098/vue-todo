<script>
import { ref } from 'vue';
import Item from './components/Item.vue';

export default {
	data(){
		return {
			newTodo: "",
			todos: [
				{
					title: "Go to the grocery",
					completed: true
				},
				{
					title: "Do the Laundry",
					completed: false
				},
				{
					title: "Walk the dog",
					completed: false
				}
			]
		}
	},
	components: {
		Item
	},
	methods: {
		addNewTodo(){
			if (this.newTodo) {
				this.todos.push({title: this.newTodo, completed: false})
				this.newTodo = ""
			}
		},
		handleRemoveTodo(todo){
			this.todos.splice(this.todos.indexOf(todo), 1)
		},
		handleEditTodo(todo){
			
			
			this.todos[this.todos.indexOf(todo)] = todo;
		}
	}

}
// const todos = ref([
	
// ])
</script>

<template>
	<div class="container">
		<div class="border rounded px-4 py-5">
			<header class="text-center flex-column my-4">
				<h1 class="mb-4 fw-bold">Todo</h1>
			</header>
			<form class="add text-center my-4">
				<div class="input-group">
					<input class="form-control" type="text" name="add" placeholder="Type yor todo here ..." v-model="newTodo" />
					<button type="button" class="btn btn-success" @click="addNewTodo">Add New</button>
				</div>
			</form>
			<ul class="list-group todos mx-auto text-light shadow-lg p-3 mb-5 bg-body-tertiary rounded">
				<Item v-for="(todo, index) in todos" :key="index" :todo="todo" @remove-todo="handleRemoveTodo" @edit-todo="handleEditTodo"></Item>
			</ul>
		</div>
	</div>
</template>

<style scoped>
header {
	line-height: 1.5;
}

.logo {
	display: block;
	margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
	header {
		display: flex;
		place-items: center;
		padding-right: calc(var(--section-gap) / 2);
	}

	.logo {
		margin: 0 2rem 0 0;
	}

	header .wrapper {
		display: flex;
		place-items: flex-start;
		flex-wrap: wrap;
	}
}
</style>
