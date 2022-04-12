<template>
		<div id="application">

				<section class="Tasks">
						<input type="text" name="taskTitle" placeholder="Task">
						<input type="number" name="taskTime" placeholder="Time" min="1" step="1">
						<button class="addTask button buttonAdd" type="submit" @click="addTask">
								<img src="./assets/plus.png" alt="addTask" style="width:25px;"/>
						</button>
				</section>

				<section v-if="tasks.length > 0" class="section_task">
						<div class="listTasks">
								<ul>
										<li v-for="(task,key) in tasks " :key="key">
												{{ task.title }} -> {{ task.time }} hrs
												<button class="deleteTask button" @click="deleteTask">
														<img src="./assets/trash.png" alt="deleteTask">
												</button>
										</li>
								</ul>
						</div>

				<setion class="time">
				<h2>Time: {{totalTime}} hrs</h2>
				</setion>
				</section>

				<section v-else class="no_tasks">
						<h2>You have no homeworks</h2>
				</section>
		</div>
</template>

<script>
export default {
		data() {
				return {
						tasks: [],
						newTask: {
								title: "",
								time: 0
						}
				}
		},

		methods: {
				addTask() {
						const title = document.getElementById("taskTitle").value;
						const time = parseInt(document.getElementById("taskTime").value);

						if (title !== '' && time !== 0) {
								this.newTask.title = title
								this.newTask.time = time
								this.tasks.push(this.newTask)

								this.newTask = {
										title: "",
										time: 0
								}
						} else {
								alert('The task and time must be correct values')
						}

						localStorage.setItem("tasks", JSON.stringify(this.tasks))
				},


				deleteTask(taskIndex) {
						const taskToDelete = taskIndex.path[2]
						const arrayTasks = Array.from(taskIndex.path[3].children)

						let index

						arrayTasks.forEach((task,key) => {
								if(task == taskToDelete) {
										index = key
								}
						})

						this.tasks.splice(index,1)
						localStorage.setItem('tasks', JSON.stringify(this.tasks))
				}
		},

		computed: {
				totalTime() {
						let total = 0
						this.tasks.forEach(task => {
								total += parseInt(task.time)
						})
						return total
				}
		},

		created() {
				const tasks = localStorage.getItem("tasks")
				if(tasks) {
						this.tasks = JSON.parse(tasks) || []
				}
		}
}

</script>

<style lang="scss">

@import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;700&display=swap');
#application {
		align-items:center;
		display: flex;
		flex-direction: row;
		font-family: 'Inter',sans-serif;
		justify-content: space-evenly;


		& .Tasks {
				align-self: start;
				display: flex;
				grid-template-areas: 
				"title time"
				"button button";
				justify-items: center;
				margin-block-start: 20px;
				width: 50%;

				input {
						border: none;
						border-bottom: 1px solid #ccc;
						font-family: 'Inter',sans-serif;
						font-size: 18px;
						outline: none;
						padding: 5px;
						width: 90%;

						& #taskTitle {
								grid-area: title;
						}

						& #taskTime {
								grid-area: time;
						}
				}

				& .addTask {
						grid-area: button;
						margin-block-start: 20px;
				}
		}

		& .section_task {
				align-items: center;
				display: flex;
				flex-direction: row;
				width: 50%;

				& .listTasks {
						& ul {
								list-style-type: none;
								padding: 0;
								pointer-events: none;

								& .deleteTask {
										pointer-events: auto;
								}

								& li {
										align-items: center;
										border-radius: 10px;
										border: 1px solid black;
										display: flex;
										justify-content: space-between;
										margin-block: 15px;
										padding: 5px;
										transition: 0.5s;
										width: 400px;

										&:hover {
												background-color: crimson;
												color: white;
												opacity: 0.9;
										}
								}
						}
				}
		}

		& .icon {
				width: 25px;
		}

		& .tiempo {
				align-self: start;
				margin-left: 25px;
				width: 50%;

				h2 {
						text-align: end;
				}
		}

		& .button {
				align-items: center;
				background: none;
				border: none;
				display: flex;
				justify-content: center;
				outline: none;

				&:hover {
						cursor: pointer;
				}
		}
}

@media screen and (max-width: 1920px) {
		#application {
				flex-direction: colum;

				& .Tasks {
						align-self: center;
						width: 100%;
				}

				& .section_task {
						justify-content: center;
				}
		}
}

@media screen and (max-width: 600px) {
		#application {
				.section_task {
						flex-direction: colum-reverse;
						& .listTasks {
								& ul {
										& li {
												width: max-content;
										}
								}
						}

						& .time {
								margin: 0;
								width: 100%;

								& h2 {
										text-align: center;
								}
						}
				}
		}
}

@media screen and (max-width: 400px) {
		#application {
				& .Tasks {
						display: flex;
						flex-direction: column;
				}
		}
}

</style>
