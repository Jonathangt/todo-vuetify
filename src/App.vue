<template>
    <v-app id="inspire">
        <v-navigation-drawer v-model="drawer" :mobile-breakpoint="768"  app>
             <v-img class="pa-4 pt-7" src="https://picsum.photos/1920/1080?random" height="170" gradient="to top right, rgba(19,84,122,.5), rgba(128,208,199,.8)">
                <v-avatar size="70" class="mb-2">
                    <img src="https://ui-avatars.com/api/?name=Jonathan" gradient="to top right, rgba(19,84,122,.5), rgba(128,208,199,.8)" alt="Jonathan" height="170"/>
                    <!-- <img src="https://ui-avatars.com/api/?name=Jonathan" alt="Jonathan" /> -->
                </v-avatar>
                <div class="white--text text-subtitle-1 font-weight-bold">
                    Jonathan
                </div>
               <!--  <div class="white--text text-subtitle-2">
                    Jonathangt
                </div> -->
            </v-img>

            <v-divider></v-divider>

            <v-list dense nav>
                <v-list-item v-for="item in items" :key="item.title" :to="item.to" link>
                    <v-list-item-icon>
                        <v-icon>{{ item.icon }}</v-icon>
                    </v-list-item-icon>

                    <v-list-item-content>
                        <v-list-item-title>{{ item.title }}</v-list-item-title>
                    </v-list-item-content>
                </v-list-item>
            </v-list>
        </v-navigation-drawer>

        <v-app-bar app color="primary" dark shrink-on-scroll src="https://picsum.photos/1920/1080?random" prominent :height="$route.path === '/' ? '240' : '170'"> <!-- scroll-target="#scrolling-techniques-2" -->
            <template v-slot:img="{ props }">
                <v-img v-bind="props" gradient="to top right, rgba(19,84,122,.5), rgba(128,208,199,.8)"></v-img>
            </template>

            <v-container class="">
                <v-row>
                    <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>
                    <v-spacer></v-spacer>
                    <search />
                </v-row>
                <v-row>
                    <v-toolbar-title class="text-h4 ml-4">Todo App</v-toolbar-title>
                </v-row>
                <v-row>
                    <live-date-time />
                </v-row>
                <v-row v-if="$route.path === '/'">
                    <field-add-task />
                </v-row>
            </v-container>

        </v-app-bar>

        <v-main>
            <router-view></router-view>
            <snackbar />
        </v-main>
    </v-app>
</template>

<script>
    import FieldAddTask from "./components/Todo/FieldAddTask.vue";
    import LiveDateTime from './components/Tools/LiveDateTime.vue'
    import Search from './components/Tools/Search.vue'
    import Snackbar from './components/Shared/Snackbar.vue'


    export default {
        data: () => ({
            drawer: true,
            items: [
                { title: "Todo", icon: "mdi-format-list-checks", to: "/" },
                { title: "About", icon: "mdi-help-box", to: "/about" },
            ],
            right: null,
        }),
        components: {
            FieldAddTask,
            LiveDateTime,
            Search,
            Snackbar,
        },
        mounted() {
            this.$store.dispatch('getTasks')
        },
        created() {
            console.clear()
        },
    };
</script>

<style lang="sass">
    .header-container
        max-width: none
</style>
