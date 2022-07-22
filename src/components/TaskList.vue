<template>
    <ul class="list-group">
        <li v-for="(task, index) in tasks" :key="index" @click="$router.push(`/tasks/${task._id}`)"
            class="list-group-item list-group-item-action">
            {{ index + 1 }}.
            {{ task.title }}
        </li>
    </ul>
</template>

<script lang="ts">
import { Task } from '@/interfaces/Task';
import { getTasks } from '@/services/TasksServices'
import { defineComponent, onMounted, ref } from 'vue'

export default defineComponent({
    name: 'Task-list',
    setup() {

        const tasks = ref<Task[]>([]);
        const getAllTasks = async () => {
            const res = await getTasks();
            tasks.value = res.data
            console.log(res);
        };

        onMounted(getAllTasks)

        return { tasks }
    }
})
</script>