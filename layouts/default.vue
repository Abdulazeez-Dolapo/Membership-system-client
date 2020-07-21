<template>
  <v-app>
    <v-navigation-drawer
      v-model="drawer"
      :mini-variant="miniVariant"
      :clipped="clipped"
      fixed
      app
    >
      <v-list>
        <v-list-item to="/" router exact>
          <v-list-item-action>
            <v-icon>mdi-apps</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title v-text="'Home'" />
          </v-list-item-content>
        </v-list-item>

        <v-list-item to="/profile" router exact v-if="$auth.$state.loggedIn">
          <v-list-item-action>
            <v-icon>mdi-chart-bubble</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title v-text="'Profile'" />
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-app-bar :clipped-left="clipped" fixed app class="elevation-0">
      <v-app-bar-nav-icon @click.stop="drawer = !drawer" />
      <v-toolbar-title class="hover" @click="home" v-text="title" />
      <v-spacer />
      <v-btn text to="/login" class="ma-0" v-if="!$auth.$state.loggedIn">
        Login
      </v-btn>

      <v-btn text @click="logout" class="ma-0" v-else>
        Logout
      </v-btn>

      <template v-if="$auth.$state.loggedIn">
        <v-btn :to="`/profile`" class="text-capitalize" text>
          {{ $auth.$state.user.username }}
        </v-btn></template
      >
    </v-app-bar>

    <v-main>
      <v-container fluid>
        <nuxt />
      </v-container>
    </v-main>

    <v-footer :fixed="fixed" app>
      <v-row class="ma-0 justify-center">
        <a
          href="https://www.linkedin.com/in/abdulazeezabdulrafiudolapo96"
          target="_blank"
          rel="noopener noreferrer"
          >Abdulazeez Dolapo Abdulrafiu &copy; {{ new Date().getFullYear() }}</a
        >
      </v-row>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  data() {
    return {
      clipped: false,
      drawer: false,
      fixed: false,
      miniVariant: false,
      title: "Members App"
    };
  },
  methods: {
    logout() {
      this.$auth.logout();
    },
    home() {
      this.$router.push("/");
    }
  }
};
</script>
<style>
.hover:hover {
  cursor: pointer;
}
</style>
