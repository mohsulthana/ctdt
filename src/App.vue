<template>
  <v-app>
    <v-navigation-drawer app width="320">
      <v-list-item @click="routeTo('/')">
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
        <div
          @click="routeTo('existing-container')"
          v-if="this.$route.path.includes('/existing-container')"
        >
          <v-list-item>
            <v-list-item-icon>
              <v-icon>mdi-cog</v-icon>
            </v-list-item-icon>
            <v-list-item-content>
              Existing Container Terminal
            </v-list-item-content>
          </v-list-item>
          <v-list-item>
            <v-list-item-content>
              <v-row>
                <v-col
                  v-for="(value, index) in 8"
                  :key="index"
                  cols="12"
                  sm="4"
                >

                  <router-link
                    tag="button"
                    :to="{ name: 'stepper', query: { id: index }}"
                    style="
                      background-color: #0e2d61;
                      padding: 1rem;
                      text-align: center;
                      color: white;
                      border-radius: 4px;
                    "
                  >
                    {{ `Step ${index + 1}` }}
                  </router-link>
                </v-col>
              </v-row>
            </v-list-item-content>
          </v-list-item>
        </div>

        <!-- New Container -->
        <div v-else-if="this.$route.path.includes('/new-container')" @click="routeTo('new-container')">
          <v-list-item>
            <v-list-item-icon>
              <v-icon>mdi-cog</v-icon>
            </v-list-item-icon>
            <v-list-item-content> New Container Terminal </v-list-item-content>
          </v-list-item>
          <v-list-item>
            <v-list-item-content>
              <v-row>
                <v-col
                  v-for="(value, index) in 8"
                  :key="index"
                  cols="12"
                  sm="4"
                >
                  <div
                    style="
                      background-color: #0e2d61;
                      padding: 1rem;
                      text-align: center;
                      color: white;
                      border-radius: 4px;
                    "
                  >
                    {{ `Step ${index + 1}` }}
                  </div>
                </v-col>
              </v-row>
            </v-list-item-content>
          </v-list-item>
        </div>
      </v-list>
    </v-navigation-drawer>

    <v-main>
      <router-view></router-view>
    </v-main>
  </v-app>
</template>

<script>
export default {
  name: "App",
  data: () => ({
    items: [
      { title: "Dashboard", icon: "mdi-view-dashboard" },
      { title: "Account", icon: "mdi-account-box" },
      { title: "Settings", icon: "mdi-cog" },
    ],
  }),
  methods: {
    routeTo(args) {
      this.$router.push(args);
    },
  },
  computed: {
    routerPath: function() {
      return this.$router.currentRoute.path
    }
  }
};
</script>

<style>
.v-text-field__suffix {
  color: #0E2D61;
}
</style>