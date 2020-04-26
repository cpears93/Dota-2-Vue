<template>
  <div id="app">
    <dota2-header title="Dota2" />
    <dota2-header v-if="!heroes.length" title="LOADING..." />
    <div id="list-info" v-if="heroes.length">
      <vuedog-beer-list :beers="beers"></vuedog-beer-list>
      <vuedog-beer-info
        v-if="selectedBeer"
        :beer="selectedBeer"
      ></vuedog-beer-info>
    </div>
    <vuedog-favourites-list :favourites="favourites"></vuedog-favourites-list>
  </div>
</template>

<script>
import { eventBus } from "@/main.js";
import Dota2Heroes from "@/components/Dota2Heroes";
import Dota2Matches from "@/components/Dota2Matches";
import Dota2Rankings from "@/components/Dota2Rankings";

export default {
  name: "app",
  components: {
    "dota2-header": Dota2Header,
    "dota2-matches": Dota2Matches,
    "dota2-list": Dota2Rankings
  },
  data() {
    return {
      matches: [],
      selectedBeer: null
    };
  },
  computed: {
    favourites: function() {
      return this.matches.filter(matches => matches.isFavourite);
    }
  },
  methods: {
    getBeers: function() {
      fetch("https://api.punkapi.com/v2/beers")
        .then(res => res.json())
        .then(beerData => {
          beerData.forEach(beer => (beer.isFavourite = false));
          this.beers = beerData;
        })
        .then(() => this.sortBeers("name"));
    },
    sortBeers: function(property) {
      this.beers.sort((a, b) => {
        return a[property] < b[property] ? -1 : 1;
      });
    },
    markFavourite: function(beer) {
      const index = this.beers.indexOf(beer);
      this.beers[index].isFavourite = true;
    }
  },
  mounted() {
    this.getBeers();

    eventBus.$on("beer-selected", beer => (this.selectedBeer = beer));

    eventBus.$on("favourite-added", beer => this.markFavourite(beer));
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
