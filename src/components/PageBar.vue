<template>
  <v-app id="inspire">
    <v-navigation-drawer v-model="drawer" app>
      <v-list>
        <v-list-item class="d-flex justify-center pt-6 mt-6">
          <v-list-item-avatar>
            <v-icon color="light-blue">fa-regular fa-user</v-icon>
          </v-list-item-avatar>
        </v-list-item>

        <v-list-item>
          <v-list-item-content class="text-center">
            <v-list-item-title class="text-h4">
              {{ getLoggedUser.username }}
            </v-list-item-title>
            <v-list-item-title class="text-h5">
              {{ getLoggedUser.fullName }}
            </v-list-item-title>
            <v-list-item-subtitle>{{
              getLoggedUser.email
            }}</v-list-item-subtitle>
          </v-list-item-content>
        </v-list-item>
      </v-list>

      <v-divider class="light-blue"></v-divider>

      <v-list dense nav>
        <v-list-item v-for="item in items" :key="item.title" link>
          <v-list-item-icon color="light-blue">
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title>{{ item.title }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-app-bar
      absolute
      color="light-blue"
      dark
      shrink-on-scroll
      prominent
      src="https://picsum.photos/1920/1080?random"
      fade-img-on-scroll
      scroll-target="#scrolling-techniques-3"
    >
      <template v-slot:img="{ props }">
        <v-img
          v-bind="props"
          color="light-blue"
          gradient="to top right, rgba(25,32,72,.7), rgb(0,191,255)"
        ></v-img>
      </template>

      <v-app-bar-nav-icon
        class="white--text text-caption"
        @click="drawer = !drawer"
      ></v-app-bar-nav-icon>
      <v-app-bar-title>TODO Vuetify </v-app-bar-title>

      <v-spacer></v-spacer>

      <v-btn icon>
        <v-icon>mdi-magnify</v-icon>
      </v-btn>

      <v-btn icon>
        <v-icon>mdi-heart</v-icon>
      </v-btn>

      <v-btn icon :to="{ name: 'home' }">
        <v-icon>mdi-dots-vertical</v-icon>
      </v-btn>
    </v-app-bar>

    <v-main>
      <router-view></router-view>
    </v-main>
  </v-app>
</template>

<script>
export default {
  data: () => ({
    drawer: null,
    items: [
      { title: 'Dashboard', icon: 'mdi-view-dashboard' },
      { title: 'Photos', icon: 'mdi-image' },
      { title: 'About', icon: 'mdi-help-box' },
    ],
  }),
  computed: {
    getLoggedUser() {
      // pega a string salva pelo login
      const userStr = localStorage.getItem('user')
      // converte de string salva no locastore para objeto JS, assim podemos user2.username
      const user = JSON.parse(userStr)
      return user
    },
  },
}
</script>
