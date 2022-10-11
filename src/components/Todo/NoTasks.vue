<template>
    <div class="no-tasks">
        <v-icon size="100" color="primary">
            mdi-check
        </v-icon>
        <div class="text-h5 primary--text">No tasks</div>
    </div>
</template>

<style lang="sass" scoped>
    .no-tasks
        left: 50%
        position: absolute
        top: 50%
        transform: translate(-50%, -50%)
    .sorting
        bottom: 20px
        left: 50%
        position: fixed
        transform: translateX(-50%)
</style>