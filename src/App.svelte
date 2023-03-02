<script>
	import TodoHeader from './components/TodoHeader.svelte';
	import TodoInfo from './components/TodoInfo.svelte';
	import TodoList from './components/TodoList.svelte';

	import {v4 as uuid} from 'uuid';

	let todos = [
		{
			id :uuid(),
			content: "첫 번째 할 일",
			done: false
		},
		{
			id :uuid(),
			content: "두 번째 할 일",
			done: false
		},
		{
			id :uuid(),
			content: "세 번째 할 일",
			done: true
		},
		{
			id :uuid(),
			content: "네 번째 할 일",
			done: false
		},
	]

	let todoValue = '';

	let handleCheckTodo = (id) => {
		todos = todos.map(todo => {
			if(todo.id === id) { // 선택된 todo 값 찾기
				todo.done = !todo.done; // 선택된 todo의 done 상태 변경
			}
			return todo;
		})
	}

	let addTodoItem = () => {
		console.log("todoValue",todoValue)
		if(todoValue) {
			const newTodo = {
				id: uuid(),
				content: todoValue,
				done: true,
			}
			todos = [...todos, newTodo];
			todoValue = '';
		}
	}

	let handleTodoInputKeyup = (e) => {
		if(e.keyCode === 13) { // 엔터키 발동 시 value값 등록 후 메소드 실행
			console.log(`todoValue: ${e.target.value}`)
			todoValue = e.target.value;

			addTodoItem();
		}
	} 
</script>

<div class="app">
	<TodoHeader {todoValue} {handleTodoInputKeyup} />
	<TodoInfo />
	<TodoList {todos} {handleCheckTodo}/> <!--handleCheckTodo Props로 넘김-->
</div>