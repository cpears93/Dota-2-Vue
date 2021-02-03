<template lang="html">
  <div class="rankings-list" v-if="rankingses.length">
    <dota2-rankings-list-item
      v-for="(rankings, index) in rankings"
      :hero="rankings"
      :key="index"
    >
  </dota2-rankings-list-item>
  </div>
</template>

<script>

export default {
  name: "dota2-rankings-list",
  props: ["rankings"],
  componets: {
    "dota2-rankings-list-item": Dota2RankingsListItem
  }
};
</script>

<style lang="css" scoped>
</style>
