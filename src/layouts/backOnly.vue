<template>
    <v-app id="inspire">
        <v-app-bar app
                   :elevation="$vuetify.breakpoint.lgAndUp ? 4 : '' "
                   :dark="dark"
                   :color="navColor"
                   :elevate-on-scroll="!$vuetify.breakpoint.lgAndUp">
            <v-btn icon
                   :color="iconColor"
                   @click="$router.go(-1)">
                <v-icon>mdi-arrow-left</v-icon>
            </v-btn>
            <v-toolbar-title class="pa-0 font-weight-bold">
                {{ title }}
            </v-toolbar-title>
            <v-spacer/>
            <LinkBtn v-if="leftBtn.type === 'link'" :color="leftBtn.color" :text="leftBtn.text" :link="leftBtn.link"/>
        </v-app-bar>
        <v-content class="grey lighten-5">
            <slot></slot>
        </v-content>
    </v-app>
</template>

<script>
import {serverBus} from '@/main';
import LinkBtn from "@/layouts/LinkBtn";

export default {
    name: "BackOnly",
    components: {LinkBtn},
    data() {
        return {
            title: '',
            navColor: 'white',
            iconColor: 'pink',
            dark: false,
            leftBtn : {}
        }
    },
    created() {
        // Using the server bus
        serverBus.$on('navProps', (props) => {
            this.title = props.title
            this.navColor = props.color
            this.dark = props.dark
            this.iconColor = props.iconColor
            this.leftBtn = props.leftBtn || {}
        });
    }
}
</script>

<style>
    .container {
        max-width: 700px
    }
</style>
