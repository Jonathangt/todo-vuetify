<template>
    <div class="home">
        <list-tasks v-if="$store.state.tasks.length" />

        <no-tasks v-else />

        <button-done-sorting v-if="$store.state.sorting" />
    </div>
</template>

<script>
    import ListTasks from "../components/Todo/ListTasks.vue";
    import NoTasks from "../components/Todo/NoTasks.vue";
    import ButtonDoneSorting from "../components/Todo/ButtonDoneSorting.vue";

    export default {
        name: "Home",

        components: {
            ListTasks,
            NoTasks,
            ButtonDoneSorting,
        },
        data: () => ({
            newTask: "",
        }),
        methods: {
            addTask() {
                this.$store.commit("addTask", this.newTask);
                this.newTask = "";
            },
        },
    };
</script>
