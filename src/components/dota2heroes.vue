<template>
  <div id="hero-info-container">
    <dota2-header :title="hero.name" />
    <div id="hero-info">
      <div id="picture">
        <dota2-hero-image :imageUrl="hero.image_url"></dota2-hero-image>
      </div>
      <div id="hero-text">
        <p>{{ hero.description }}</p>
        <p>{{ hero.rating }}</p>
      </div>
    </div>
  </div>
</template>

<script>
import { eventBus } from "@/main.js";
import Dota2Header from "@/components/Dota2Header";
import Dota2Image from "@/components/Dota2Image";

export default {
  props: ["hero"],
  components: {
    "dota2-header": Dota2Header,
    "dota2-hero-image": Dota2HeroImage
  }
};
</script>
<style scoped>
#hero-info-container {
  width: 55%;
}

#hero-info {
  display: flex;
}

p {
  font: 13px Futura;
}

li {
  font: 10px Futura;
}

#picture {
  display: flex;
  flex-direction: column;
  width: 200px;
  padding: 20px;
}

#hero-text {
  margin-left: 10%;
  margin-right: 10%;
  word-wrap: normal;
}

img {
  height: 325px;
  width: 150px;
}

h3 {
  font: bold 15px Futura;

}
</style>
