<script setup>
import { ref } from 'vue';
let tasks = ref([])  // ref对象 任务列表 { name: '任务名', state: '状态' } active completed
let taskName = ref("")  // ref对象 .value
// 添加任务
function addTask() {
  if (taskName.value.trim() === '') {
    return
  }
  tasks.value.push({
    name: taskName.value,
    state: 'active'
  })
  taskName.value = ""
}
// 完成任务
function completeTask(index) {
  tasks.value[index].state = 'completed'
}
// 删除任务
function deleteTask(index) {
  tasks.value.splice(index, 1)
}
// 删除所有
function deleteAll() {
  tasks.value.splice(0, tasks.value.length)
}
</script>

<template>
  <!-- value属性 -->
  <input type="text" placeholder="请输入任务" v-model="taskName" v-on:keyup.enter="addTask">
  <p v-if="tasks.length === 0">还没有任务，请添加。</p>
  <div>
    <p v-for="(task,index) in tasks" v-bind:class="task.state" v-on:click="completeTask(index)" v-on:dblclick="deleteTask(index)">{{ index+1 }}. {{ task.name }}</p>
  </div>
  <span>共 {{ tasks.length }} 个</span> <button v-on:click="deleteAll">清理</button>
</template>

<style scoped>
</style>
