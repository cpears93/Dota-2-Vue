<template>
  <div id="app">
    <dota2-header title="Dota2" />
    <dota2-header v-if="!heroes.length" title="LOADING..." />
    <div id="list-info" v-if="heroes.length">
      <dota2-heroes :heroes="heroes"></dota2-heroes>
      <dota2-rankings
        v-if="selectedHero"
        :heroes="selectedHero"
      ></dota2-rankings>
    </div>
    <dota2-matches-list :matches="matches"></dota2-matches-list>
  </div>
</template>

<script>
import { eventBus } from "@/main.js";
import Dota2Heroes from "@/components/dota2Heroes";
import Dota2Matches from "@/components/dota2Matches";
import Dota2Rankings from "@/components/dota2Rankings";

export default {
  name: "app",
  components: {
    "dota2-header": Dota2Header,
    "dota2-matches": Dota2Matches,
    "dota2-rankings": Dota2Rankings,
    "dota2-heroes":Dota2Heroes
  },
  data() {
    return {
      matches: [],
      selectedMatch: null
    };
  },
  computed: {
    matches: function() {
      return this.matches.filter(matches => matches.isMatches);
    }
  },
  methods: {
    getHeroes: function() {
      fetch("https://api.opendota.com/api")
        .then(res => res.json())
        .then(heroData => {
          heroData.forEach(hero => (hero.isHero = false));
          this.heroes = heroData;
        })
        .then(() => this.sortHeroes("name"));
    },
    sortHeroes: function(property) {
      this.heroes.sort((a, b) => {
        return a[property] < b[property] ? -1 : 1;
      });
    },
    markMatch: function(dota2) {
      const index = this.dota2.indexOf(dota2);
      this.dota2[index].isMatches = true;
    }
  },
  mounted() {
    this.getDota2();

    eventBus.$on("hero-selected", dota2 => (this.selectedDota2 = dota2));

    eventBus.$on("match-added", dota2 => this.markMatch(dota2));
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
