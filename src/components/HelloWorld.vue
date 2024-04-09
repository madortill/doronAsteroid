<template>
  <div class="greetings">
    <div> {{ times }} </div>
    <button @click="onClick">click me</button>
  </div>
</template>


<script>
  export default {
    data() {
      return {
        // clicks: 0
      }
    },
    props: ["times"],
    emits: ["increase"],
    methods: {
      onClick () {
        this.$emit('increase');
      }
    }
  }
</script>

<style scoped>
h1 {
  font-weight: 500;
  font-size: 2.6rem;
  top: -10px;
}

h3 {
  font-size: 1.2rem;
}

.greetings h1,
.greetings h3 {
  text-align: center;
}

@media (min-width: 1024px) {
  .greetings h1,
  .greetings h3 {
    text-align: left;
  }
}
</style>
