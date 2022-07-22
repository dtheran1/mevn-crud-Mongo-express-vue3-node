<template>
    <div class="col-md-4 offset-md-4">
        <form @submit.prevent="handleUpdate($route.params.id as string)" class="card card-body">
            <h1 class="text-center h-3 mb-3">Task Details</h1>
            <input type="text" v-model="currentTask.title" class="form-control mb-3">
            <textarea rows="3" v-model="currentTask.description" class="form-control mb-3"></textarea>
            <button class="btn btn-primary">Update</button>
        </form>
        <div class="text-center">
            <button @click="handleDelete($route.params.id as string)" class="btn btn-danger">Delete</button>
        </div>
    </div>
</template>

<script lang="ts">
import { Task } from "@/interfaces/Task";
import router from "@/router";
import { deleteTask, getTask, updateTask } from "@/services/TasksServices";
import { defineComponent, onMounted, reactive, ref } from "vue";
import { useRoute } from "vue-router";


export default defineComponent({
    name: "details-component",
    setup() {
        const route = useRoute();
        const currentTask = ref<Task>({
            title: '',
            description: '',
            done: false,
            _id: ''
        });
        const getTaskById = async (id: string) => {
            const res = await getTask(id);
            currentTask.value = res.data
        }
        const handleUpdate = async (id: string) => {
            await updateTask(id, currentTask.value);
            router.push('/')
        };

        const handleDelete = async (id: string) => {
            await deleteTask(id)
            router.push('/')
        };

        onMounted(() => {
            getTaskById(route.params.id as string);
        });
        return { currentTask, handleUpdate, handleDelete }
    }
})
</script>