<template>
    <v-dialog :value="true" persistent max-width="290">
        <v-card>
            <v-card-title class="text-h5">
                Edit task?
            </v-card-title>
            <v-card-text>
                Edit the tittle of this task:
                <v-text-field v-model="taskTitle" @keyup.enter="saveTask" />
            </v-card-text>
            <v-card-actions>
                <v-spacer></v-spacer>
                <v-btn color="black darken-1" text @click="$emit('close')">
                    Cancel
                </v-btn>
                <v-btn color="red darken-1" text @click="saveTask" :disabled="taskTitleInvalid">
                    Save
                </v-btn>
            </v-card-actions>
        </v-card>
    </v-dialog>
</template>


<script>
    export default {
        data:() => ({
            taskTitle: null,
        }),
        props: {
            task: {
                type: Object,
                require: true,
                default: () => {},
            },
        },
        computed: {
            taskTitleInvalid(){
                return !this.taskTitle
            }
        },
        methods: {
            saveTask(){
                if (this.taskTitleInvalid) {
                    return
                }
                const payload = {
                    id: this.task.id,
                    title: this.taskTitle,
                }
                this.$store.dispatch('updateTaskTitle', payload)
                this.$emit('close')
                this.$vuetify.goTo(0, { duration: 0} )
            }
        },
        mounted() {
            this.taskTitle = this.task.title
        },
    };
</script>