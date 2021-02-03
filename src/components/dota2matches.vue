<template lang="html">
  <div class="match-list" v-if="matches.length">
    <dota2-match-list-item
      v-for="(match, index) in match"
      :hero="match"
      :key="index"
    >
  </dota2-match-list-item>
  </div>
</template>

<script>

export default {
  name: "dota2-match-list",
  props: ["match"],
  componets: {
    "dota2-match-list-item": Dota2MatchListItem
  }
};
</script>

<style lang="css" scoped>

.hero-list {
  width: 40%;
  height: 600px;
  overflow-y: scroll;
  display: flex;
  flex-wrap: wrap;
}
</style>
