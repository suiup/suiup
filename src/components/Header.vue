<template>
    <div style="height: 48px">
        <v-app-bar
                color="blue-grey lighten-2"
                dense
                fixed
                dark
        >
            <v-app-bar-nav-icon></v-app-bar-nav-icon>
            <v-tab :to="blog.route">
                {{blog.text}}
            </v-tab>
            <v-tab :to="album.route">
                {{album.text}}
            </v-tab>
            <v-tab :to="articles.route">
                {{articles.text}}
            </v-tab>
            <v-tab :to="about.route">
                {{about.text}}
            </v-tab>
            <v-spacer></v-spacer>
            <v-tab router :to="links.route">
                {{links.text}}
            </v-tab>
            <v-tab router :to="layout.route">
                {{layout.text}}
            </v-tab>
            <v-btn icon>
                <v-icon>mdi-heart</v-icon>
            </v-btn>

            <v-btn icon>
                <v-icon>mdi-magnify</v-icon>
            </v-btn>

            <v-menu
                    left
                    bottom
            >
                <template v-slot:activator="{ on, attrs }">
                    <v-btn
                            icon
                            v-bind="attrs"
                            v-on="on"
                    >
                        <v-icon>mdi-dots-vertical</v-icon>
                    </v-btn>
                </template>

                <v-list>
                    <v-list-item router :to="theme.route">
                        <v-list-item-title>Theme</v-list-item-title>
                    </v-list-item>
                    <v-list-item :to="color.route">
                        <v-list-item-title>Color</v-list-item-title>
                    </v-list-item>
                    <v-list-item :to="markdown.route">
                        <v-list-item-title>Markdown preview</v-list-item-title>
                    </v-list-item>
                    <v-list-item :to="article.route">
                        <v-list-item-title>Articles</v-list-item-title>
                    </v-list-item>
                </v-list>
            </v-menu>
        </v-app-bar>
    </div>
</template>

<script>
    export default {
        name: "Header",
        data() {
            return {
                blog: {
                    text: "Robin's Blog",
                    route: "/suiup"
                },
                about: {
                    text: "About",
                    route: "/about"
                },
                links: {
                    text: "Calendar",
                    route: "/calendars"
                },
                album:{
                    text: "Album",
                    route: "/album"
                },
                articles:{
                    text: "Articles",
                    route: "/articles"
                },
                fileR:{
                    text: "Articles",
                    route: "/articles"
                },
                theme: {
                    route:"/theme"
                },
                color: {
                    route: "/color"
                },
                markdown:{
                    route: "/markdown"
                },
                article: {
                    route: "/article"
                },
                layout: {
                    text: "Layout",
                    route: "/layout"
                }
            }
        }
    }
</script>

<style scoped>
    .v-tab{
        margin: 10px;
    }
    .v-tab { text-transform: none !important; color: white; text-decoration: none}
</style>