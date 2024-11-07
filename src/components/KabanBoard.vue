<template>
    <div>
        <h3>{{ msg }}</h3>
    </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import vuedraggable from "vuedraggable";

export default defineComponent({
    name: "KabanBoard",
    props: {
        msg: String,
    },
    setup() {
        const columns = [
            {
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
                title: "Sprint Backlog",
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
                title: "Review",
                tasks: [
                    {
                        id: 9,
                        title: "Test checkout flow",
                        date: "Sep 15",
                        type: "QA",
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
                title: "Done",
                tasks: [
                    {
                        description: "Task 7",
                    },
                    {
                        description: "Task 8",
                    },
                ],
            },
        ];
        return {
            columns,
        };
    },
});
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>
