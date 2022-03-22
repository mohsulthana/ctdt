<template>
  <v-app>
    <v-app-bar color="green" class="flex-grow-0" app dark>
      <v-app-bar-title>Coding Beauty</v-app-bar-title>
    </v-app-bar>
    <v-navigation-drawer app width="320">
      <v-list-item>
        <v-list-item-content>
          <v-img
            lazy-src="@/assets/ctdt.png"
            height="100%"
            width="auto"
            src="@/assets/ctdt.png"
          ></v-img>
        </v-list-item-content>
      </v-list-item>
      <v-list dense nav>
        <v-list-item v-for="item in items" :key="item.title" link>
          <v-list-item-icon>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title>{{ item.title }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-main>
      <v-container>
        <steps v-for="(value, index) in 2" :key="index" />
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
import Steps from "./components/Steps.vue";

export default {
  components: { Steps },
  name: "App",
  data: () => ({
    items: [
      { title: "Dashboard", icon: "mdi-view-dashboard" },
      { title: "Account", icon: "mdi-account-box" },
      { title: "Settings", icon: "mdi-cog" },
    ],
  }),
};
</script>