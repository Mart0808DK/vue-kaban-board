<template>
    <div class="flex justify-center">
        <div class="min-h-screen flex overflow-x-scroll py-12">
            <div v-for="column in columns" :key="column.id" class="bg-gray-100 rounded-lg px-3 py-3 column-width rounded mr-4">
                <h3 class="text-gray-700 font-semibold tracking-wide">{{ column.title }}</h3>
                <div class="mt-4">
                    <draggable :list="column.tasks" class="flex flex-col" group="tasks" ghost-class="ghost-card" @change="onTaskChange">
                        <template #item="{ element: task }">
                            <TaskCard :task="task" />
                        </template>
                    </draggable>
                </div>
            </div>
        </div>
    </div>
</template>

<script lang="ts">
import { defineComponent, ref } from "vue";
import TaskCard from "./TaskCard.vue";
import draggable from "vuedraggable";

interface Task {
    id: number;
    title: string;
    date: string;
    type: string;
}
interface Column {
    id: number;
    title: string;
    tasks: Task[];
}

interface DraggableEvent {
    removed?: {
        element: Task;
        oldIndex: number;
    };
    added?: {
        element: Task;
        newIndex: number;
    };
}
export default defineComponent({
    name: "KabanBoard",
    components: {
        TaskCard,
        draggable,
    },
    setup() {
        let columns = ref<Column[]>([
            {
                id: 1,
                title: "Product Backlog",
                tasks: [
                    {   
                        id: 1,
                        title: "Add discount code to checkout page",
                        date: "Sep 14",
                        type: "Feature Request",
                    },
                    {   
                        id: 2,
                        title: "Provide documentation on integrations",
                        date: "Sep 12",
                        type: "Backend",
                    },
                    {   
                        id: 3,
                        title: "Design shopping cart dropdown",
                        date: "Sep 9",
                        type: "Design",
                    },
                    {   
                        id: 4,
                        title: "Add discount code to checkout page",
                        date: "Sep 14",
                        type: "Feature Request",
                    },
                    {   
                        id: 5,
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
                        id: 6,
                        title: "Design shopping cart dropdown",
                        date: "Sep 9",
                        type: "Design",
                    },
                    {   
                        id: 7,
                        title: "Add discount code to checkout page",
                        date: "Sep 14",
                        type: "Feature Request",
                    },
                    {   
                        id: 8,
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
                        id: 9,
                        title: "Provide documentation on integrations",
                        date: "Sep 12",
                        type: "Backend",
                    },
                    {
                        id: 10,
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
                        id: 11,
                        title: "Provide documentation on integrations",
                        date: "Sep 12",
                        type: "Backend",
                    },
                    {   
                        id: 12,
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
                        id: 13,
                        title: "Provide documentation on integrations",
                        date: "Sep 12",
                        type: "Backend",
                    },
                    {   
                        id: 14,
                        title: "Design shopping cart dropdown",
                        date: "Sep 9",
                        type: "Design",
                    },
                ],
            },
        ]);

        
        
        const onTaskChange = (event: DraggableEvent) => {
            if (event.removed) {
                const task = event.removed.element;
                const oldIndex = event.removed.oldIndex;
                const columnId = columns.value.findIndex((column) => column.tasks.includes(task));
                columns.value[columnId].tasks.splice(oldIndex, 1);
                console.log("Task removed from column", columnId);
            }
            if (event.added) {
                const task = event.added.element;
                const newIndex = event.added.newIndex;
                const columnId = columns.value.findIndex((column) => column.tasks.includes(task));
                columns.value[columnId].tasks.splice(newIndex, 0, task);
                console.log("Task added to column", columnId);
            }
            
            
        };
    

        return {
            columns,
            onTaskChange,
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
