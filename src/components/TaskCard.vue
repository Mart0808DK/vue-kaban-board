<template>
    <div class="bg-white shadow rounded px-3 pt-3 pb-5 border border-white mb-4">
        <div class="flex justify-between">
            <p class="text-gray-700 font-semibold font-sans tracking-wide text-sm">{{ task.title }}</p>
        </div>
        <p class="text-gray-600 text-sm mt-2">{{ task.description }}</p>
        <div class="flex mt-4 justify-between items-center">
            <span class="text-sm text-gray-600">{{ task.date }}</span>
            <span class="text-sm text-gray-600">{{ task.type }}</span>
        </div>
        <div class="flex justify-between">
            <button @click="showEditModal(task.id)" class="bg-gray-500 hover:bg-gray-400 text-white font-semi py-2 px-4 rounded mt-4">Edit</button>
            <button @click="removeTask(task.id)" class="bg-gray-400 hover:bg-gray-300 text-white font-semi py-2 px-4 rounded mt-4">Delete</button>
        </div>
        <TaskForm v-if="isEditModalVisible" :task="task" @submit="handleEditSubmit" @close="isEditModalVisible = false" />
    </div>
</template>

<script lang="ts">
import { defineComponent, ref } from "vue";
import TaskForm from "./TaskForm.vue";
import { Task} from "./KabanBoard.vue";

export default defineComponent({
    name: "TaskCard",
    props: {
        task: {
            type: Object,
            required: true,
        },
    },
    components: {
        TaskForm,
    },
    setup(_, { emit }) {
        const isEditModalVisible = ref(false);

        const removeTask = (id: number) => {
            emit("remove-task", id);
        };

        const showEditModal = (id: number) => {
            emit("edit-task", id);
            isEditModalVisible.value = true;
        };

        const handleEditSubmit = (updatedTask: Task) => {
            emit("edit-task", updatedTask);
            isEditModalVisible.value = false;
        };
        

        return {
            isEditModalVisible,
            handleEditSubmit,
            showEditModal,
            removeTask,
        };
    },
});



</script>
