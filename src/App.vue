<template>
		<div id="application">
				<section class="tasks">
						<input type="text" name="taskTitle" placeholder="Task">
						<input type="number" name="taskTime" placeholder="Time" min="1" step="1">
						<button class="addTask button buttonAdd" type="submit" @click="addTask">
								<img src="./assets/plus.png" alt="addTask" style="width:25px;"/>
						</button>
				</section>

				<section v-if="tasks.length > 0" class="section_task">
						<div class="listTasks">
								<ul>
										<li v-for="(task,key) in tasks " :key="key"></li>
										{{task.title}} -> {{task.time}} time
										<button class="deleteTask button" @click="deleteTask">
												<img src="./assets/trash.png" alt="deleteTask">
										</button>
								</ul>
						</div>
				<setion class="time">
				<h2>Time: {{totalTime}} hrs</h2>
				</setion>

				</section>
						</div>
</template>

<script>


</script>

<style>
.buttonAdd {
		padding: 0;
}


</style>
