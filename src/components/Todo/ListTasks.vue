<template>
    <v-list class="pt-0" flat>
       <!--  <task v-for="task in $store.getters.tasksFiltered" :key="task.id" :task="task" />
 -->
         <draggable v-model="tasks" handle=".handle">
            <task v-for="task in tasks" :key="task.id" :task="task" />
        </draggable>
    </v-list>
</template>

<script>
    import Task from "./Task.vue";
    import draggable from "vuedraggable";

    export default {
        components: {
            draggable,
            Task,
        },
         computed: {
            tasks: {
                get() {
                    return this.$store.getters.tasksFiltered;
                },
                set(value) {
                    this.$store.dispatch("setTasks", value);
                },
            },
        },
    };
</script>