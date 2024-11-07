<template>
    <div class="fixed inset-0 flex items-center justify-center bg-black bg-opacity-50 z-50">
        <div class="bg-white rounded-lg shadow-lg p-6 w-full max-w-md transform transition-transform duration-300 scale-100">
            <h3 class="text-lg font-semibold mb-4">Add Column Title</h3>
            <input @keyup.enter="addColumn" type="text" v-model="title" class="border border-gray-300 p-2 w-full mb-4" placeholder="Enter column title" />
            <div class="flex justify-between">
                <button @click="addColumn" class="bg-blue-500 hover:bg-blue-400 text-white font-bold py-2 px-4 rounded mr-2">Add Column</button>
                <button @click="closeModal" class="bg-gray-500 hover:bg-gray-400 text-white font-bold py-2 px-4 rounded">Close</button>
            </div>
        </div>
    </div>
</template>

<script>
import { defineComponent, ref } from "vue";

export default defineComponent({
    name: "AddColumnForm",
    setup(_, { emit }) {
        const title = ref("");

        const addColumn = () => {
            emit("add-column", title.value);
            title.value = "";
        };

        const closeModal = () => {
            emit("close");
        };

        return {
            title,
            addColumn,
            closeModal,
        };
    },
});
</script>