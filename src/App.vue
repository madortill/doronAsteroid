<template>

  <div class="wrapper" >
  <div class="forMedia"></div>
    <open-screen v-if ="page === 0" @next-page = "nextPage"></open-screen>
    <asteroid-definition v-if ="page === 1" @next-page = "nextPage"></asteroid-definition>
    <asteroid-types v-if ="page === 2" @next-page = "nextPage"></asteroid-types>
    <asteroid-explosion v-if ="page === 3" @next-page = "nextPage"></asteroid-explosion>
    <game v-if ="page === 4" @next-page = "nextPage"></game>
    <end-screen v-if ="page >= 5" @to-start = "toStart"></end-screen>

    

  </div>

</template>

<script>
import openScreen from './components/openScreen.vue';
import asteroidDefinition from './components/asteroidDefinition.vue';
import asteroidTypes from './components/asteroidTypes.vue';
import asteroidExplosion from './components/asteroidExplosion.vue';
import game from './components/game.vue';
import endScreen from './components/endScreen.vue';

export default {

  name: "app",
  components: {
    openScreen,
    asteroidDefinition,
    asteroidTypes,
    asteroidExplosion,
    game,
    endScreen,
  },

  data() {
    return {
      page: 0,
    };
  },
 
  methods: {
    nextPage() {
      this.page++;
    },
    toStart() {
      this.page = 0;
    },

  },
  computed: {
   
  }
}
</script>

<style scoped>
header {
  line-height: 1.5;
  max-height: 100vh;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

nav {
  width: 100%;
  font-size: 12px;
  text-align: center;
  margin-top: 2rem;
}

nav a.router-link-exact-active {
  color: var(--color-text);
}

nav a.router-link-exact-active:hover {
  background-color: transparent;
}

nav a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}

nav a:first-of-type {
  border: 0;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  nav {
    text-align: left;
    margin-left: -1rem;
    font-size: 1rem;

    padding: 1rem 0;
    margin-top: 1rem;
  }
}

@media (min-width: 768px) {
    /* העיצוב שאתה רוצה להסתיר */
    .forMedia {
      background-color: black;
      top: 0;
      left: 0;
      position: absolute;
     
    }
  }
</style>
