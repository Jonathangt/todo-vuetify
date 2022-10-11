<template>
    <v-dialog :value="true" persistent max-width="290">
        <v-card>
            <v-card-title class="text-h5">
                Delete task?
            </v-card-title>
            <v-card-text>are you sure you want to delete the task?.</v-card-text>
            <v-card-actions>
                <v-spacer></v-spacer>
                <v-btn color="black darken-1" text @click="$emit('close')">
                    No
                </v-btn>
                <v-btn color="red darken-1" text @click="$store.dispatch('deleteTask', task.id)">
                    Yes
                </v-btn>
            </v-card-actions>
        </v-card>
    </v-dialog>
</template>

<script>
    export default {
        data:() => ({
            dialog: false,
        }),
        props: {
            task: {
                type: Object,
                require: true,
                default: () => {},
            },
        },
    };
</script>