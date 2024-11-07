<template>
    <div class="bg-white shadow rounded px-3 pt-3 pb-5 border border-white mb-4">
        <div class="flex justify-between">
            <p class="text-gray-700 font-semibold font-sans tracking-wide text-sm">{{ task.title }}</p>
        </div>
        <div class="flex mt-4 justify-between items-center">
            <span class="text-sm text-gray-600">{{ task.date }}</span>
            <span class="text-sm text-gray-600">{{ task.type }}</span>
        </div>
    </div>
</template>

<script>
import { defineComponent } from "vue";

export default defineComponent({
    name: "TaskCard",
    props: {
        task: {
            type: Object,
            required: true,
        },
    },
});
</script>
