<template>
  <v-flex xs12>
    <v-card>
      <v-card-title primary-title>
        <div>
          <h3 class="headline">{{ name }}</h3>
          <v-menu
            transition="slide-x-transition"
            bottom
            left
          >
            <v-btn 
              slot="activator" 
              icon>
              <v-icon>settings</v-icon>
            </v-btn>
            <v-list>
              <v-list-tile
                @click="ruleForm()"
              >
                <v-list-tile-title>Edit</v-list-tile-title>
              </v-list-tile>
              <v-list-tile
                @click="removeRule()"
              >
                <v-list-tile-title>Delete</v-list-tile-title>
              </v-list-tile>
            </v-list>
          </v-menu>
 
          <div>{{ pattern }}</div>
            
        </div>
      </v-card-title>
      <v-card-actions>
        <v-switch
          v-model="switchEnabled" />
        <v-spacer/>
        <div class="text-xs-center">
          <v-chip 
            v-for="method in methods" 
            :key="method">{{ method }}</v-chip>
        </div>
      </v-card-actions>
    </v-card>
  </v-flex>
</template>

<script>
import router from '../router';

export default {
  name: 'RuleCard',
  props: {
    id: { type: String, default: '' },
    name: { type: String, default: 'undefined' },
    pattern: { type: String, default: 'undefined' },
    methods: { type: Array, default: () => [] },
    enabled: { type: Boolean, default: () => true },
  },
  computed: {
    switchEnabled: {
      get() {
        return this.enabled;
      },
      set() {
        this.$store.dispatch('toggleRule', this.id);
      },
    },
  },
  methods: {
    ruleForm() {
      router.push({ name: 'EditRule', params: { id: this.id } });
    },
    removeRule() {
      this.$store.dispatch('removeRule', this.id);
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.card {
  margin: 5px 0;
  .menu {
    position: absolute;
    top: 0;
    right: 0;
  }
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
