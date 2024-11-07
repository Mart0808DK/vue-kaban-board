<template>
    <div class="flex justify-center">
        <div class="min-h-screen flex overflow-x-scroll py-12">
            <div v-for="column in columns" :key="column.id" class="bg-gray-100 rounded-lg px-3 py-3 column-width rounded mr-4">
                <h3 class="text-gray-700 font-semibold tracking-wide">{{ column.title }}</h3>
                <div class="mt-4">
                    <draggable :list="column.tasks" class="flex flex-col" group="tasks" ghost-class="ghost-card">
                        <template #item="{ element: task }">
                            <TaskCard :task="task" />
                        </template>
                    </draggable>
                </div>
                <div>
                    <button @click="handleAddTask(column.id)" class="bg-gray-500 hover:bg-gray-400 text-white font-bold py-2 px-4 rounded">Add Task</button>
                </div>
            </div>
            <div class="">
              <button @click="showModal = true" class="bg-gray-500 hover:bg-gray-400 text-white font-bold py-2 px-4 rounded">Add Column</button>
            <AddColumnForm v-if="showModal" @add-column="handleAddColumn" @close="showModal = false" />
            </div>
        </div>
    </div>
</template>

<script lang="ts">
import { defineComponent, ref } from "vue";
import TaskCard from "./TaskCard.vue";
import draggable from "vuedraggable";
import AddColumnForm from "./AddColomnForm.vue";
export default defineComponent({
    name: "KabanBoard",
    components: {
        TaskCard,
        draggable,
        AddColumnForm,
    },
    setup() {
        let showModal = ref(false);
        let columns = ref([
            {
                id: 1,
                title: "Product Backlog",
                tasks: [
                    {
                        title: "Add discount code to checkout page",
                        date: "Sep 14",
                        type: "Feature Request",
                    },
                    {
                        title: "Provide documentation on integrations",
                        date: "Sep 12",
                    },
                    {
                        title: "Design shopping cart dropdown",
                        date: "Sep 9",
                        type: "Design",
                    },
                    {
                        title: "Add discount code to checkout page",
                        date: "Sep 14",
                        type: "Feature Request",
                    },
                    {
                        title: "Test checkout flow",
                        date: "Sep 15",
                        type: "QA",
                    },
                ],
            },
            {
                id: 2,
                title: "In Progress",
                tasks: [
                    {
                        title: "Design shopping cart dropdown",
                        date: "Sep 9",
                        type: "Design",
                    },
                    {
                        title: "Add discount code to checkout page",
                        date: "Sep 14",
                        type: "Feature Request",
                    },
                    {
                        title: "Provide documentation on integrations",
                        date: "Sep 12",
                        type: "Backend",
                    },
                ],
            },
            {
                id: 3,
                title: "Blocked",
                tasks: [
                    {
                        title: "Provide documentation on integrations",
                        date: "Sep 12",
                        type: "Backend",
                    },
                    {
                        title: "Design shopping cart dropdown",
                        date: "Sep 9",
                        type: "Design",
                    },
                ],
            },
            {
                id: 4,
                title: "Review",
                tasks: [
                    {
                        title: "Provide documentation on integrations",
                        date: "Sep 12",
                        type: "Backend",
                    },
                    {
                        title: "Design shopping cart dropdown",
                        date: "Sep 9",
                        type: "Design",
                    },
                ],
            },
            {
                id: 5,
                title: "Done",
                tasks: [
                    {
                        title: "Provide documentation on integrations",
                        date: "Sep 12",
                        type: "Backend",
                    },
                    {
                        title: "Design shopping cart dropdown",
                        date: "Sep 9",
                        type: "Design",
                    },
                ],
            },
        ]);

        console.log(columns.value);
        

        function handleAddTask(columnId: number) {
            columns.value[columnId-1].tasks.push({
                title: "New Task",
                date: "Sep 16",
                type: "Feature Request",
            });
          
        }

         function handleAddColumn(title: string) {
          const newId = columns.value.length > 0 ? Math.max(...columns.value.map(c => c.id)) + 1 : 1;
            columns.value.push({
                id: newId,
                title: title,
                tasks: [],
            });
            showModal.value = false;
            
          
        }

    

        return {
            columns,
            handleAddColumn,
            showModal,
            handleAddTask
        };
    },
});
</script>

<style scoped>
.column-width {
    min-width: 320px;
    width: 320px;
}
.ghost-card {
    opacity: 0.5;
    background: #f7fafc;
    border: 1px solid #4299e1;
}
</style>
