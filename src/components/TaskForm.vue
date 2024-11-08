<template>
    <div class="fixed inset-0 flex items-center justify-center bg-black bg-opacity-5 z-50">
        <div class="bg-white rounded-lg shadow-lg p-6 w-full max-w-md transform transition-transform duration-300 scale-100">
            <h3 class="text-lg font-semibold mb-4">Edit Task</h3>
            <form @submit.prevent="saveTask">
                <input 
                    v-model="localTask.title" 
                    placeholder="Title" 
                    class="border border-gray-300 p-2 w-full mb-4" 
                    required 
                />
                <textarea 
                    v-model="localTask.description" 
                    placeholder="Description" 
                    class="border border-gray-300 p-2 w-full mb-4" 
                    required 
                ></textarea>
                <input 
                    v-model="localTask.date" 
                    type="string" 
                    class="border border-gray-300 p-2 w-full mb-4" 
                    required 
                />
                <input 
                    v-model="localTask.type" 
                    placeholder="Type" 
                    class="border border-gray-300 p-2 w-full mb-4" 
                    required 
                />
                <div class="flex justify-between">
                    <button type="submit" class="bg-blue-500 hover:bg-blue-400 text-white font-bold py-2 px-4 rounded mr-2">Save</button>
                    <button type="button" @click="$emit('close')" class="bg-gray-500 hover:bg-gray-400 text-white font-bold py-2 px-4 rounded">Cancel</button>
                </div>
            </form>
        </div>
    </div>
</template>

<script lang="ts">
import { defineComponent, ref } from "vue";

export default defineComponent({
    name: "TaskForm",
    props: {
        task: {
            type: Object,
            required: true,
        },
    },
    setup(props, { emit }) {
        const updatedTask = ref({ ...props.task });
        

        const saveTask = () => {
            emit("submit", { ...updatedTask.value });
        };

        return {
            localTask: updatedTask,
            saveTask,
        };
    },
});
</script>

<style scoped>
</style>