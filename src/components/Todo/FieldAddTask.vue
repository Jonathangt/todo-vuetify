<template>
    <v-text-field v-model="newTask" placeholder="Add task" class="field-add-task pa-3" @keyup.enter="addTask" outlined label="Add Task" append-icon="mdi-plus" hide-details clearable>
        <template v-slot:append>
            <v-icon @click="addTask" color="primary" :disabled="newTaskInvalid">
                mdi-plus
            </v-icon>
        </template>
    </v-text-field>
</template>

<script>
    export default {
        data: () => ({
            newTask: "",
        }),
        computed: {
            newTaskInvalid() {
                return !this.newTask;
            },
        },
        methods: {
            addTask() {
                if (this.newTaskInvalid) {
                    return;
                }

                this.$store.dispatch("addTask", this.newTask);
                this.newTask = "";
            },
        },
    };
</script>

<style lang="sass">
    .field-add-task.v-input--is-focused
        .v-input__slot
            background: rgba(31,94,129, 0.5)
</style>