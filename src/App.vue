<template>
	<div class="container">
		<Header @toggle-add-task="toggleAddTask" text="Task Tracker" :showAddTask="showAddTask" />
		<div v-if="showAddTask">
			<AddTask @add-task="addTask" />
		</div>
		<Tasks @toggle-reminder="toggleReminder" @delete-task="deleteTask" :tasks="tasks" />
	</div>
</template>

<script>
	import Header from "./components/Header.vue";
	import Tasks from "./components/Tasks.vue";
	import AddTask from './components/AddTask.vue';

	export default {
		name : 'App',
		components : {
			Header,
			Tasks,
			AddTask,
		},
		data(){
			return {
				tasks : [],
				showAddTask: false,
			}
		},
		created(){
			this.tasks = [
				{
					id: 1,
					text: 'Doctors Appointment',
					day: 'March 1st at 2:30pm',
					reminder: true,
				},
				{
					id: 2,
					text: 'Metting at school',
					day: 'Aguest 4th at 2:30am',
					reminder: true,
				},
				{
					id: 3,
					text: 'Date Out',
					day: 'July 1st at 7:30pm',
					reminder: false,
				}
			];
		},
		methods: {
			addTask(task){
				this.tasks = [...this.tasks, task];
			},
			toggleReminder(id){
				this.tasks = this.tasks.map((task => task.id === id ? {...task, reminder: !task.reminder} : task));
			},
			deleteTask(id) {
				if(confirm('are you sure?'))
					this.tasks = this.tasks.filter((task => task.id !== id));
			},
			toggleAddTask(){
				this.showAddTask = !this.showAddTask;
			}
		}
	}
</script>

<style>
	@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300&display=swap');

	* {
		box-sizing: border-box;
		margin: 0;
		padding: 0
	}

	body {
		font-family: 'Poppins', Arial, Helvetica, sans-serif
	}

	.container {
		max-width: 500px;
		margin: 30px auto;
		overflow: auto;
		min-height: 300px;
		border: 1px solid steelblue;
		padding: 30px;
		border-radius: 5px;
	}

	.btn {
		display: inline-block;
		background: black;
		color: white;
		border: none;
		padding: 10px 20px;
		margin: 5px;
		border-radius: 5px;
		cursor: pointer;
		text-decoration: none;
		font-size: 15px;
		font-family: inherit;
	}

	.btn:focus {
		outline: none;
	}

	.btn:active {
		transform: scale(0.98);
	}

	.btn-block
	{
		display: block;
		width: 100%;
	}

</style>
