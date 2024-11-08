<template>
    <div class="flex justify-center">
        <div class="min-h-screen flex overflow-x-scroll py-12">
            <div v-for="column in columns" :key="column.id" class="bg-gray-100 rounded-lg px-3 py-3 column-width rounded mr-4">
                <h3 class="text-gray-700 font-semibold tracking-wide">{{ column.title }}</h3>
                <div class="mt-4">
                    <draggable :list="column.tasks" class="flex flex-col" group="tasks" ghost-class="ghost-card" @change="onTaskChange">
                        <template #item="{ element: task }">
                            <TaskCard :task="task" @edit-task="updateTask" @remove-task="removeTask" />
                        </template>
                    </draggable>
                </div>
                <div>
                    <button @click="handleAddTask(column.id)" class="bg-gray-500 hover:bg-gray-400 text-white font-bold py-2 px-4 rounded">Add Task</button>
                </div>
            </div>
            <div>
                <button @click="showModal = true" class="bg-gray-500 hover:bg-gray-400 text-white font-bold py-2 px-4 rounded">+</button>
                <AddColumnForm v-if="showModal" @add-column="handleAddColumn" @close="showModal = false" />
            </div>
        </div>
    </div>
</template>

<script lang="ts">
import { defineComponent, ref, onMounted, watch } from "vue";
import TaskCard from "./TaskCard.vue";
import draggable from "vuedraggable";
import AddColumnForm from "./AddColomnForm.vue";

export interface Task {
    id: number;
    title: string;
    description: string;
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
                                description: "Add a field for users to enter a discount code on the checkout page.",
                                date: "Sep 14",
                                type: "Feature Request",
                            },
                            {
                                id: 2,
                                title: "Provide documentation on integrations",
                                description: "Write documentation on how to integrate with our API.",
                                date: "Sep 12",
                                type: "Backend",
                            },
                            {
                                id: 3,
                                title: "Design shopping cart dropdown",
                                description: "Design a dropdown for the shopping cart in the header.",
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
                                id: 4,
                                title: "Redesign landing page",
                                description: "Create a new design for the landing page.",
                                date: "Sep 10",
                                type: "Design",
                            },
                            {
                                id: 5,
                                title: "Implement user profile page",
                                description: "Create a user profile page with user information.",
                                date: "Sep 11",
                                type: "Frontend",
                            },
                            {
                                id: 6,
                                title: "Fix bugs in user profile page",
                                description: "Fix bugs in the user profile page.",
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
                                id: 7,
                                title: "Add payment gateway integration",
                                description: "Integrate a payment gateway for processing payments.",
                                date: "Sep 13",
                                type: "Backend",
                            },
                            {
                                id: 8,
                                title: "Update product images",
                                description: "Update product images on the website.",
                                date: "Sep 12",
                                type: "Design",
                            },
                            {
                                id: 9,
                                title: "Optimize site performance",
                                description: "Optimize",
                                date: "Sep 14",
                                type: "Backend",
                            },
                            {
                                id: 10,
                                title: "Review code for security vulnerabilities",
                                description: "Review code for security vulnerabilities.",
                                date: "Sep 15",
                                type: "Backend",
                            },
                            {
                                id: 11,
                                title: "Update product descriptions",
                                description: "Update product descriptions on the website.",
                                date: "Sep 13",
                                type: "Content",
                            },
                            {
                                id: 12,
                                title: "Add new feature to product page",
                                description: "Add a new feature to the product page.",
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
                                id: 13,
                                title: "Fix bugs in user profile page",
                                description: "Fix bugs in the user profile page.",
                                date: "Sep 11",
                                type: "Bug",
                            },
                            {
                                id: 14,
                                title: "Update product images",
                                description: "Update product images on the website.",
                                date: "Sep 12",
                                type: "Design",
                            },
                            {
                                id: 15,
                                title: "Optimize site performance",
                                description: "Optimize",
                                date: "Sep 14",
                                type: "Backend",
                            },
                            {
                                id: 15,
                                title: "Review code for security vulnerabilities",
                                description: "Review code for security vulnerabilities.",
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
                                id: 16,
                                title: "Provide documentation on integrations",
                                description: "Write documentation on how to integrate with our API.",
                                date: "Sep 12",
                                type: "Backend",
                            },
                            {
                                id: 17,
                                title: "Design shopping cart dropdown",
                                description: "Design a dropdown for the shopping cart in the header.",
                                date: "Sep 9",
                                type: "Design",
                            },
                        ],
                    },
                ];
            }
        });

        const updateTask = (updatedTask: Task) => {
            columns.value.forEach(column => {
                const taskIndex = column.tasks.findIndex(task => task.id === updatedTask.id);
                if (taskIndex !== -1) {
                    column.tasks[taskIndex] = updatedTask;
                }
            });
            saveColumnsToLocalStorage();
        };

        const saveColumnsToLocalStorage = () => {
            localStorage.setItem("columns", JSON.stringify(columns.value));
        };

        const removeTask = (taskId: number) => {
            for (const column of columns.value) {
                const taskIndex = column.tasks.findIndex(task => task.id === taskId);
                if (taskIndex !== -1) {
                    column.tasks.splice(taskIndex, 1);
                    break;
                }
            }
        };
        function handleAddTask(columnId: number) {
            const newId = columns.value[columnId - 1].tasks.length > 0 ? Math.max(...columns.value[columnId - 1].tasks.map(t => t.id)) + 1 : 1;
            columns.value[columnId - 1].tasks.push({
                id: newId,
                title: "New Task",
                description: "Description of the task",
                date: "Sep 15",
                type: "Feature Request",
            });
        }

        function handleAddColumn(title: string) {
            const newId = columns.value.reduce((maxId, column) => Math.max(maxId, column.id), 0) + 1;
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
                const columnId = columns.value.findIndex(column => column.tasks.includes(task));
                columns.value[columnId].tasks.splice(oldIndex, 1);
            }
            if (event.added) {
                const task = event.added.element;
                const newIndex = event.added.newIndex;
                const columnId = columns.value.findIndex(column => column.tasks.includes(task));
                columns.value[columnId].tasks.splice(newIndex, 0, task);
            }
        };

        watch(
            columns,
            newColumns => {
                localStorage.setItem("columns", JSON.stringify(newColumns));
            },
            { deep: true }
        );

        return {
            columns,
            showModal,
            updateTask,
            handleAddTask,
            onTaskChange,
            handleAddColumn,
            removeTask,
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
