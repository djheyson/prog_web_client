<template>
  <div>
    <v-navigation-drawer v-model="drawer" fixed temporary app
      class="lighten-2"
      disable-resize-watcher>
      <v-img :aspect-ratio="16/9" src="https://cdn.vuetifyjs.com/images/parallax/material2.jpg">
        <v-row align="end" class="lightbox white--text pa-0 fill-height fill-width">
          <v-list class="pa-0">
            <v-list-item>
              <v-list-item-avatar color="white">
                <v-icon :color="'primary'">mdi-account-circle</v-icon>
              </v-list-item-avatar>

              <v-list-item-content>
                <v-list-item-title>{{ user().name }}</v-list-item-title>
                <v-list-item-subtitle v-text="user().email"></v-list-item-subtitle>
              </v-list-item-content>
            </v-list-item>
          </v-list>
        </v-row>
      </v-img>

      <v-divider></v-divider>

      <v-list dense>
        <v-list-item v-for="item in items" :key="item.title" link :to="item.url">
          <v-list-item-icon>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title>{{ item.title }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-app-bar app color="blue" dense dark>
      <v-app-bar-nav-icon @click.stop="drawer = !drawer"></v-app-bar-nav-icon>

      <v-toolbar-title>Page title</v-toolbar-title>

      <div class="flex-grow-1"></div>

      <v-btn icon>
        <v-icon @click.stop="logout">mdi-logout</v-icon>
      </v-btn>
    </v-app-bar>
  </div>
</template>

<script>
export default {
  name: 'AppNavigation',
  data() {
    return {
      drawer: false,
      group: null,
      items: [
        {
          title: 'Home',
          url: '/',
          icon: 'mdi-home',
        },
        {
          title: 'Archives',
          url: '/archives',
          icon: 'mdi-file',
        },
        {
          title: 'Profile',
          url: '/profile',
          icon: 'mdi-account',
        },
        {
          title: 'Profile Update',
          url: '/profile/update',
          icon: 'mdi-account',
        },
      ],
    };
  },
  computed: {
    isAuthenticated() {
      return this.$store.getters.isAuthenticated;
    },
  },
  watch: {
    group() {
      this.drawer = false;
    },
  },
  methods: {
    logout() {
      this.$store.dispatch('signOut');
    },
    user() {
      return this.$store.state.user;
    },
  },
};
</script>

<style scoped>
</style>
