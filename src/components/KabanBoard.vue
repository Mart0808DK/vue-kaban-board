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
            </div>
        </div>
    </div>
</template>

<script lang="ts">
import { defineComponent, ref } from "vue";
import TaskCard from "./TaskCard.vue";
import draggable from "vuedraggable";
export default defineComponent({
    name: "KabanBoard",
    components: {
        TaskCard,
        draggable,
    },
    setup() {
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
                        type: "Backend",
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

    

        return {
            columns,
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
