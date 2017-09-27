<template>
    <div id="app">
        <md-toolbar>
            <md-button class="md-icon-button" @click="toggle">
                <md-icon>menu</md-icon>
            </md-button>

            <h2 class="md-title">
                VueStagram
            </h2>
        </md-toolbar>

        <md-sidenav class="md-left" md-swipeable ref="sidenav">
            <md-list>
                <md-list-item v-for="menu in menus" :key="menu.path" @click.native="toggle">
                    <router-link :to="menu.path">
                        <md-icon>{{menu.icon}}</md-icon>
                        <span>{{menu.title}}</span>
                    </router-link>
                </md-list-item>
            </md-list>
        </md-sidenav>

        <div id="contents">
            <router-view></router-view>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'app',
        methods: {
            toggle() {
                this.$refs.sidenav.toggle()
            }
        },
        data() {
            return {
                menus: [
                    {
                        path: '/me',
                        icon: 'person',
                        title: 'My Info'
                    },
                    {
                        path: '/feeds',
                        icon: 'list',
                        title: 'My Feeds'
                    },
                    {
                        path: '/tagSearch',
                        icon: 'search',
                        title: 'Tag Search'
                    },
                ]
            }
        }
    }
</script>

<style>
    #contents {
        padding: 16px;
    }
</style>
