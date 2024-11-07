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
import { defineComponent, ref, onMounted, watch } from "vue";
import TaskCard from "./TaskCard.vue";
import draggable from "vuedraggable";

interface Task {
    id: number;
    title: string;
    date: string;
    type?: string;
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
        
        
        const columns = ref<Column[]>([]);

        // function handleAddTask(columnId: number) {
        //     columns.value[columnId-1].tasks.push({
        //         title: "New Task",
        //         date: "Sep 16",
        //         type: "Feature Request",
        //     });
          
        // }

         function handleAddColumn(title: string) {
          const newId = columns.value.length > 0 ? Math.max(...columns.value.map(c => c.id)) + 1 : 1;
            columns.value.push({
                id: newId,
                title: title,
                tasks: [],
            });
            showModal.value = false;
         }

         const onTaskChange = (event: DraggableEvent) => {
            if (event.removed) {
                const task = event.removed.element;
                const oldIndex = event.removed.oldIndex;
                const columnId = columns.value.findIndex((column) => column.tasks.includes(task));
                columns.value[columnId].tasks.splice(oldIndex, 1);
            }
            if (event.added) {
                const task = event.added.element;
                const newIndex = event.added.newIndex;
                const columnId = columns.value.findIndex((column) => column.tasks.includes(task));
                columns.value[columnId].tasks.splice(newIndex, 0, task);
            }
            console.log("Columns", columns.value);
        };
            
          
    
            onMounted(() => {
                const storedColumns = localStorage.getItem("columns");
                if (storedColumns) {
                    columns.value = JSON.parse(storedColumns);
                } else {
                    columns.value = [
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
                            ],
                        },
                        {
                            id: 2,
                            title: "In Progress",
                            tasks: [
                                {
                                    id: 1,
                                    title: "Redesign landing page",
                                    date: "Sep 10",
                                    type: "Design",
                                },
                                {
                                    id: 2,
                                    title: "Implement user profile page",
                                    date: "Sep 11",
                                    type: "Frontend",
                                },
                                {
                                    id: 3,
                                    title: "Fix bugs in user profile page",
                                    date: "Sep 11",
                                    type: "Bug",
                                },
                            ],
                        },
                        {
                            id: 3,
                            title: "Blocked",
                            tasks: [
                                {
                                    id: 1,
                                    title: "Add payment gateway integration",
                                    date: "Sep 13",
                                    type: "Backend",
                                },
                                {
                                    id: 2,
                                    title: "Update product images",
                                    date: "Sep 12",
                                    type: "Design",
                                },
                                {
                                    id: 3,
                                    title: "Optimize site performance",
                                    date: "Sep 14",
                                    type: "Backend",
                                },
                                {
                                    id: 4,
                                    title: "Review code for security vulnerabilities",
                                    date: "Sep 15",
                                    type: "Backend",
                                },
                                {
                                    id: 5,
                                    title: "Update product descriptions",
                                    date: "Sep 13",
                                    type: "Content",
                                },
                                {
                                    id: 6,
                                    title: "Add new feature to product page",
                                    date: "Sep 15",
                                    type: "Feature Request",
                                },
                            ],
                        },
                        {
                            id: 4,
                            title: "Review",
                            tasks: [
                                {
                                    id: 1,
                                    title: "Fix bugs in user profile page",
                                    date: "Sep 11",
                                    type: "Bug",
                                },
                                {
                                    id: 2,
                                    title: "Update product images",
                                    date: "Sep 12",
                                    type: "Design",
                                },
                                {
                                    id: 3,
                                    title: "Optimize site performance",
                                    date: "Sep 14",
                                    type: "Backend",
                                },
                                {
                                    id: 4,
                                    title: "Review code for security vulnerabilities",
                                    date: "Sep 15",
                                    type: "Backend",
                                },
                            ],
                        },
                        {
                            id: 5,
                            title: "Done",
                            tasks: [
                                {
                                    id: 1,
                                    title: "Provide documentation on integrations",
                                    date: "Sep 12",
                                    type: "Backend",
                                },
                                {
                                    id: 2,
                                    title: "Design shopping cart dropdown",
                                    date: "Sep 9",
                                    type: "Design",
                                },
                            ],
                        },
                    ];
                }
            });

            
    
            watch(columns, (newColumns) => {
                localStorage.setItem("columns", JSON.stringify(newColumns));
            }, { deep: true });
    
            return {
                columns,
                // handleAddTask,
                onTaskChange,
                showModal,
                handleAddColumn,
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
