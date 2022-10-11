<template>
    <div>
        <v-menu bottom left>
            <template v-slot:activator="{ on, attrs }">
                <v-btn icon v-bind="attrs" v-on="on" color="">
                    <v-icon>mdi-dots-vertical</v-icon>
                </v-btn>
            </template>

            <v-list>
                <v-list-item v-for="(item, i) in items" :key="i" @click="handleClick(i)">
                    <v-list-item-icon>
                        <v-icon v-text="item.icon"> </v-icon>
                    </v-list-item-icon>
                    <v-list-item-title>{{ item.title }}</v-list-item-title>
                </v-list-item>
            </v-list>
        </v-menu>

        <dialog-edit v-if="dialogs.edit" :task="task" @close="dialogs.edit = false" />

        <dialog-due-date v-if="dialogs.dueDate" @close="dialogs.dueDate = false" :task="task" />

        <dialog-delete v-if="dialogs.delete" :task="task" @close="dialogs.delete = false" />

    </div>
</template>

<script>
    import DialogDelete from "./Dialogs/DialogDelete.vue";
    import DialogEdit from "./Dialogs/DialogEdit.vue";
    import DialogDueDate from "./Dialogs/DialogDueDate.vue";

    export default {
        props: {
            task: {
                type: Object,
                require: true,
                default: () => {},
            },
        },
        data: () => ({
            items: [{
                    title: 'Edit',
                    icon: 'mdi-pencil',
                    click(){ this.dialogs.edit = true  },

                },
                {
                    title: 'Due date',
                    icon: 'mdi-calendar',
                    click(){  this.dialogs.dueDate = true },
                },
                {
                    title: 'Delete',
                    icon: 'mdi-delete',
                    click(){ this.dialogs.delete = true  },
                },
                {
                    title: 'Sort',
                    icon: 'mdi-drag-horizontal-variant',
                    click() {
                        if (!this.$store.state.search){
                            this.$store.commit('toggleSorting')
                        }else{
                            this.$store.commit('showSnackbar', 'How DARE you try to sort while searching!' )
                        }
                    }
                }
            ],
            dialogs: {
                edit: false,
                dueDate: false,
                delete: false,
            },
        }),
        components: {
            DialogDelete,
            DialogDueDate,
            DialogEdit,
        },
        methods: {
            handleClick(index){
                this.items[index].click.call(this)
            }
        },
    };
</script>
