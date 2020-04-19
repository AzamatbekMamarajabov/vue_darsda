<template>
  <v-app id="inspire">
    <v-navigation-drawer
      v-model="drawerRight"
      app
      clipped
      right
      class="mb-0 pb-0"
    >
      <v-list dense>
        <v-list-item @click.stop="settings = !settings">
          <v-list-item-action>
            <v-icon>mdi-settings</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title>Settings</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
      <v-footer app>
        <span>Darsda</span>

        <v-spacer />

        <span>&copy; </span>
      </v-footer>
    </v-navigation-drawer>

    <v-app-bar app clipped-right color="cyan darken-3" dark>
      <v-app-bar-nav-icon @click.stop="drawer = !drawer" />
      <v-toolbar-title>Darsda</v-toolbar-title>
      <v-spacer />
      <v-btn icon @click.stop="drawerRight = !drawerRight" class="mr-1"
        ><v-icon>mdi-account</v-icon></v-btn
      >
    </v-app-bar>

    <v-navigation-drawer v-model="drawer" app>
      <v-list dense>
        <v-list-item @click.stop="left = !left">
          <v-list-item-action>
            <v-icon>mdi-exit-to-app</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title>Open Temporary Drawer</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-navigation-drawer v-model="left" fixed temporary />

    <v-content>
      <v-container class="fill-height" fluid>
        <v-row justify="center" align="center">
          <v-col class="shrink"> </v-col>
        </v-row>
      </v-container>
    </v-content>

    <v-navigation-drawer v-model="settings" fixed right temporary>
       <v-list-item @click.stop="settings = !settings">
          <v-list-item-action>
            <v-icon>mdi-right-bold-circle</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title>Go Back</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      <v-list-item>
        <span v-if="isLoggedIn">
          <a @click="logout"> <v-icon>mdi-logout</v-icon> Logout</a></span
        >
      </v-list-item></v-navigation-drawer
    >
  </v-app>
</template>

<script>
export default {
  props: {
    source: String,
  },

  data: () => ({
    drawer: null,
    drawerRight: false,
    settings: false,
    left: false,
  }),

  computed: {
    isLoggedIn: function () {
      return this.$store.getters.isLoggedIn;
    },
  },
  methods: {
    logout: function () {
      this.$store.dispatch("logout").then(() => {
        this.$router.push("/login");
      });
    },
  },

  created: function () {
    this.$http.interceptors.response.use(undefined, function (err) {
      return new Promise(function () {
        if (err.status === 401 && err.config && !err.config.__isRetryRequest) {
          this.$store.dispatch("logout");
        }
        throw err;
      });
    });
  },
};
</script>
