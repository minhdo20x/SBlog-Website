<template>
  <v-app id="inspire">
    <v-navigation-drawer v-model="drawer" app>
      <v-list-item>
        <v-list-item-content>
          <v-list-item-title> The Review </v-list-item-title>
          <v-list-item-subtitle> Free To Confess </v-list-item-subtitle>
        </v-list-item-content>
      </v-list-item>
      <v-divider></v-divider>
      <v-list rounded dense>
        <v-list-item-group color="primary">
          <v-list-item v-for="(item, i) in items" :key="i" :to="item.link" link>
            <v-list-item-icon>
              <v-icon v-text="item.icon"></v-icon>
            </v-list-item-icon>
            <v-list-item-content>
              <v-list-item-title v-text="item.title"></v-list-item-title>
            </v-list-item-content>
          </v-list-item>
        </v-list-item-group>
      </v-list>
    </v-navigation-drawer>

    <v-app-bar app>
      <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>

      <v-toolbar-title>The Review</v-toolbar-title>
    </v-app-bar>

    <v-main>
      <router-view></router-view>
    </v-main>
  </v-app>
</template>

<script>
import { mdiClipboardTextSearch } from "@mdi/js";
export default {
  data: () => ({
    drawer: null,
    items: [
      { title: "Home", icon: "mdi-home", link: "/" },
      { title: "Search", icon: "mdi-clipboard-text-search", link: "/About" },
      { title: "Make Content", icon: "mdi-file-plus", link: "/add-post" },
    ],
  }),
};
</script>