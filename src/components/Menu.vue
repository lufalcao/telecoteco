<template>
  <div>
    <v-list>
      <v-list-item @click="goToHello()">
        <v-list-item-content>
          <v-list-item-title>
            Página Inicial
          </v-list-item-title>
        </v-list-item-content>
      </v-list-item>
    </v-list>
    <v-list>
      <v-list-item @click="goToAbout()">
        <v-list-item-content>
          <v-list-item-title>
            Sobre este projeto
          </v-list-item-title>
        </v-list-item-content>
      </v-list-item>
    </v-list>
    <v-expansion-panels focusable flat>
      <v-expansion-panel v-for="panel in panels" :key="panel.id">
        <v-expansion-panel-header><b>{{panel.id}}</b> {{ panel.panel }}</v-expansion-panel-header>
        <v-expansion-panel-content>
          <v-list dense>
            <v-list-item-group v-model="selectedExercise" color="primary">
              <v-list-item v-for="exercise in panel.exercise_list" :key="exercise.id" :value="exercise">
                <v-list-item-content>
                  <v-list-item-title>
                    {{panel.id}}.{{exercise.id}} {{exercise.title}}
                  </v-list-item-title>
                </v-list-item-content>
              </v-list-item>
            </v-list-item-group>
          </v-list>
        </v-expansion-panel-content>
      </v-expansion-panel>
    </v-expansion-panels>
    <v-divider></v-divider>
    <v-list>
      <v-list-item @click="goToReferences()">
        <v-list-item-content>
          <v-list-item-title>
            Referências
          </v-list-item-title>
        </v-list-item-content>
      </v-list-item>
    </v-list>
  </div>
</template>

<script>
import { mapGetters, mapMutations } from "vuex";

export default {
  methods: {
    ...mapMutations(["selectExercise", 'goToReferences', 'goToHello', 'goToAbout'])
  },
  computed: {
    ...mapGetters(["panels"]),
    selectedExercise: {
      get() {
        return this.$store.state.selectedExercise;
      },
      set(value) {
        this.$store.commit("selectExercise", value);
        if(["xs", "sm"].indexOf(this.$vuetify.breakpoint.name) != -1){
          this.$store.commit("setAppDrawer", !this.$store.state.appDrawer);
        }
      }
    },
  }
};
</script> 

<style scoped>

.v-expansion-panel-header > *:not(.v-expansion-panel-header__icon) {
    flex: 0.1 1 auto;
}

</style>