<template>
  <v-app id="inspire">
    <v-app-bar
      app
      dark
      prominent
      height="50"
      src="art.jpg"
    >
      <template v-slot:img="{ props }">
        <v-img
          v-bind="props"
        ></v-img>
      </template>
      <v-container class="header-container pa-0">
          <v-row class="py-3">
            <live-date-time />
            <v-spacer></v-spacer>
            <tools-search 
              v-if="$route.path === '/'"
            />
          </v-row>
        </v-container>
    </v-app-bar>
    <v-main>
      <v-container 
        fluid 
        class="pa-0"
      >
        <router-view></router-view>
        <snackbar/>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
  export default {
    data: () => ({ 
      drawer: null,
      items: [
        { title: 'Todo', icon: 'mdi-checkbox-marked-circle-plus-outline', to: '/' }
      ]
    }),
    components: {
      'tools-search': require('@/components/Tools/Search.vue').default,
      'live-date-time': require('@/components/Tools/LiveDateTime.vue').default,
    },
    mounted() {
      this.$store.dispatch('getTasks')
    }
  }
</script>

<style lang="sass">
  .header-container
    max-width: none !important
</style>