<template>
    <div class="col-md-4 offside-md-4">
        <form @submit.prevent="saveTask" class="card card-body">
        <h1 class="text-center h-3  mb-3">Create Task</h1>
            <input v-model="task.title" type="text" placeholder="Write a title" class="form-control mb-3" autofocus>

            <textarea rows="3" placeholder="Write a Description" v-model="task.description"
                class="form-control mb-3"></textarea>

            <button 
                class="btn btn-primary"
                :disabled="!task.title || !task.description"
            >Save</button>
        </form>
    </div>
</template>

<script lang="ts">
import { defineComponent, reactive } from "vue";
import { Task } from "../interfaces/Task";
import { createTask } from "@/services/TasksServices";
import { useRouter } from "vue-router";
export default defineComponent({
    name: 'Task-form',
    setup() {
        const task = reactive({}) as Task;
        const router = useRouter();

        const saveTask = async () => {
            const res = await createTask(task)
            console.log(res);
            router.push({ name: 'tasks' });
        }


        return {
            task, saveTask
        }
    }
})

</script>