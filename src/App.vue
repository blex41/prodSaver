<template>
  <v-app>
    <div id="app">
      <v-toolbar 
        dark 
        color="primary"
      >
        <v-toolbar-side-icon 
          v-if="previousIconVisible" 
          @click.native="rulesPage()">
          <v-icon>chevron_left</v-icon>
        </v-toolbar-side-icon>
        <v-btn 
          v-else 
          flat 
          disabled 
          icon/>
        <v-toolbar-title>ProdSaver</v-toolbar-title>
      </v-toolbar>
      <router-view/>
      <v-footer>
        <v-menu 
          transition="slide-y-transition"
          top>
          <v-btn 
            slot="activator">
            <img
              :src="require(`./assets/img/${this.$store.getters.langChosen}.png`)" 
            >
          </v-btn>
          <v-list>
            <v-list-tile 
              v-for="lang in langs" 
              :key="lang"
              @click="changeLanguage(lang)">
              <img
                :src="require(`./assets/img/${lang}.png`)" 
              >     
              <v-list-tile-title>{{ lang }}</v-list-tile-title>
            </v-list-tile>
          </v-list>
        </v-menu>        
      </v-footer>
    </div>
  </v-app>
</template>

<script>
import router from './router';

export default {
  name: 'App',
  computed: {
    langs: function() {
      return this.$store.getters.langsAvailable;
    },
    previousIconVisible() {
      return this.$route.path !== '/';
    },
  },
  methods: {
    rulesPage() {
      router.push({ name: 'Rules' });
    },
    changeLanguage(lang) {
      this.$store.dispatch('changeLanguage', lang);
    },
  },
};
</script>

<style lang="scss">
body {
  height: auto;
  width: 350px;
  .container {
    padding: 0;
  }

  .application--wrap {
    min-height: initial;
  }

  .footer,
  .list {
    img {
      width: 32px;
    }

    img ~ .list__tile__title {
      padding-left: 7px;
    }
  }
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
#nav {
  padding: 30px;
  a {
    font-weight: bold;
    color: #2c3e50;
    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>
