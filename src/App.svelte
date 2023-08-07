<script>
	let todoList = [];
	let todo = '';
	let filter = 'all';

	function addTodo() {
		todoList = [{
			todo: todo,
			status : 'pending'
		}, ...todoList];

		todo = '';
		console.log(todoList)
	}

	function markComplete(i) {
		todoList[i].status = 'completed';
		todoList = [...todoList];
		console.log(todoList)
	};

	function removeTodo(i) {
		todoList.splice(i, 1);
		todoList = [...todoList];
	};

	function openAll() {
		filter = 'all';
	}

	function openCompleted() {
		filter = 'completed';
	}

	function openIncompleted() {
		filter = 'pending';
	}

</script>

<style>
	* {
		margin : 0px;
		padding: 0px;
	}

	section {
		position: relative;
		top: 0; 
    	left: 0;
		width: 100%;
		padding: 8px;
		background: #3f061b;
		display: flex;
    	justify-content: space-between;
    	align-items: center;
    	flex-direction: column;
	}

	h1 {
		font-size: 32px;
		color : white;
		padding: 1rem;
	}

	h2 {
		font-size: 24px;
		color:#b59aa4;
	}

	h3 {
		font-size: 12px;
		color: #cecece;;
	}

	footer {
		position: fixed;
		bottom: 0; 
    	left: 0;
		display: flex;
		justify-content: center;
		align-items: center;
		background-color: #b59aa4;
		height: 10vh;
		width: 100%;
	}

	footer h2 {
		color:#3f061b;
	}

	.container {
		display: flex;
		justify-content: center;
		align-items:flex-start;
		background: #3f061b;
		width:  100%;
		min-height: 32rem;
	}

	.todos {
		padding: 3rem;
		background: #b59aa4;
		border-radius: 5px;
		width: 80%;
		margin: 20px 0px;
	}

	.todos .form {
		display: flex;
	}

	.todos .form input,
	.todos .form button {
		border : 1px solid #3f061b;
		height: 3rem;
		outline: none;
		border-radius: 5px;
	}

	.todos .form input {
		flex : 1;
		text-indent: 20px;
	}

	.todos .form button {
		width : 3rem;
		margin-left: 1rem;
		cursor: pointer;
		color : #3f061b;
	}

	.todos .todo-list {
		min-height: 200px;
	}

	.todo {
		display: flex;
		flex : 1;
		justify-content: space-between;
		margin: 1rem 0;
	}

	.todo button {
		width: 25px;
		height: 25px;
		border: 1px solid #3f061b;
		color: #3f061b;
		border-radius: 5px;
		margin: 0px 5px;
		cursor: pointer;
	}

	.todo button.active {
		background: #3f061b;
		color : #b59aa4;
	}

	.filters {
		display : flex;
		justify-content: space-between;
	}

	.filters button {
		padding: 10px 8px;
		border: 1px solid #3f061b;
		color: #3f061b;
		border-radius: 5px;
		cursor: pointer;
	}

	.filters button.active {
		background: #3f061b;
		color : #b59aa4;
	}


	
</style>
<div>
<section>
	<h1>To Do</h1>
	<h2>Add your To Do Tasks</h2>
	<h3>Mark them as completed once you finish them</h3>
</section>

<div class="container">
	<div class="todos">

		<div class="form">
			<input type="text" bind:value={todo}>
			<button on:click={addTodo}>Add</button>
		</div>

		<div class="todo-list">
			{#each todoList as singleTodo, i}
				{#if filter === 'all'}

				<div class="todo">
					<div>
					{singleTodo.todo}
					</div>
		
				<div>
				<button class="{singleTodo.status === 'completed' ? 'active' : ''}" on:click={() => markComplete(i)}>
					&#10004;
				</button>

				<button on:click={() => removeTodo(i)}>
					&#10006;
				</button>
				</div>
				
				</div>

				{:else if filter === 'completed'}
					{#if singleTodo.status === 'completed'}
					<div class="todo">
						<div>
						{singleTodo.todo}
						</div>
	
					<button on:click={() => removeTodo(i)}>
						&#10006;
					</button>
					
					</div>
					{/if}
				{:else}
					{#if singleTodo.status === 'pending'}
					<div class="todo">
						<div>
						{singleTodo.todo}
						</div>
			
					<button class="{singleTodo.status === 'pending' ? 'active' : ''}" on:click={() => markComplete(i)}>
						&#10004;
					</button>
					
					</div>
					{/if}

				{/if}
				
			{/each}
		</div>

		<div class="filters">
			<button class="{filter === 'all' ? 'active' : ''}" on:click={openAll}>
				All
			</button>

			<button class="{filter === 'completed' ? 'active' : ''}" on:click={openCompleted}>
				Completed
			</button>

			<button class="{filter === 'pending' ? 'active' : ''}" on:click={openIncompleted}>
				Incompleted
			</button>

		</div>
	</div>
</div>
<footer>
	<h2>Never Give Up!</h2>
</footer>
</div>