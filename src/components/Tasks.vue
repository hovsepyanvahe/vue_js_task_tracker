<template>
    <div :key="task.id" v-for="task in tasks">
        <Task
            @toggle-reminder="$emit('toggle-reminder', task.id)"
            @delete-task="$emit('delete-task', task.id)"
            :task="task"
        /><br />
    </div>
</template>

<script>
import Task from './Task.vue';

export default {
    name: 'MainTasks',
    props: {
        tasks: Array,
    },
    components: {
        Task,
    },
    emits: ['delete-task', 'toggle-reminder'],
};
</script>
