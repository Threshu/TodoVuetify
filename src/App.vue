<template>
  <v-app id="inspire">
    <v-navigation-drawer 
      v-model="drawer" 
      :mobile-breakpoint="768"
      app
    >
      <v-img
        class="pa-4 pt-7"
        src="mountains.jpg"
        height="170"
        gradient="to top right, rgba(19,84,122,.5), rgba(128,208,199,.8)"
      >
        <v-avatar
          size="70"
          class="mb-2"
        >
          <img
            src="https://images-wixmp-ed30a86b8c4ca887773594c2.wixmp.com/f/ec405492-b7bb-4e17-af83-6902727e0271/dbt8x18-ca45894c-e69b-4c43-b96e-0477272ca12d.png?token=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJzdWIiOiJ1cm46YXBwOjdlMGQxODg5ODIyNjQzNzNhNWYwZDQxNWVhMGQyNmUwIiwiaXNzIjoidXJuOmFwcDo3ZTBkMTg4OTgyMjY0MzczYTVmMGQ0MTVlYTBkMjZlMCIsIm9iaiI6W1t7InBhdGgiOiJcL2ZcL2VjNDA1NDkyLWI3YmItNGUxNy1hZjgzLTY5MDI3MjdlMDI3MVwvZGJ0OHgxOC1jYTQ1ODk0Yy1lNjliLTRjNDMtYjk2ZS0wNDc3MjcyY2ExMmQucG5nIn1dXSwiYXVkIjpbInVybjpzZXJ2aWNlOmZpbGUuZG93bmxvYWQiXX0.kCYt-sVSuO_0szihfLxWB94OvZxG8cuuReIY3nzfbjA"
            alt="Threshu"
          >
        </v-avatar>
        <div class="white--text text-subtitle-1 font-weight-bold">
          Threshu
        </div>
        <div class="white--text text-subtitle-2">Support</div>
      </v-img>
      <v-list
        dense
        nav
      >
        <v-list-item
          v-for="item in items"
          :key="item.title"
          :to="item.to"
          link
        >
          <v-list-item-icon>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title>{{ item.title }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

     <v-app-bar
      app
      color="primary"
      dark
      src="mountains.jpg"
      prominent
      :height="($route.path === '/') ? '210' : '140'"
    >
      <template v-slot:img="{ props }">
        <v-img
          v-bind="props"
          gradient="to top right, rgba(19,84,122,.9), rgba(128,208,199,.9)"
        ></v-img>
      </template>

      <v-container class="header-container pa-0">
        <v-row>
          <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>
          <v-spacer></v-spacer>
          <search />
        </v-row>
        <v-row>
          <v-toolbar-title class="text-h4 ml-4">{{ $store.state.appTitle }}</v-toolbar-title>          
        </v-row>
        <v-row>
          <live-date-time />
        </v-row>
        <v-row v-if="$route.path === '/'">
          <field-add-task />
        </v-row>
      </v-container>
    </v-app-bar>

    <v-main>
      <router-view></router-view>
      <snackbar />
    </v-main>
  </v-app>
</template>

<script>
import Snackbar from '@/components/Shared/Snackbar.vue'
import Search from '@/components/Tools/Search.vue'
import LiveDateTime from '@/components/Tools/LiveDateTime.vue'
import FieldAddTask from '@/components/Todo/FieldAddTask.vue'

  export default {
    data: () => ({ 
        drawer: null,         
        items: [
          { title: 'Todo', icon: 'mdi-format-list-checks', to: '/' },
          { title: 'About', icon: 'mdi-help-box', to: '/about' },
        ],
    }),
    mounted() {
      this.$store.dispatch('getTasks')
    },
    components: {
      'snackbar': Snackbar,
      'search': Search,
      'live-date-time': LiveDateTime,
      'field-add-task': FieldAddTask
    }
  }
</script>

<style lang="sass">
  .header-container
    max-width: none !important

</style>