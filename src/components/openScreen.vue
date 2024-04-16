<template>
    <div id="open-screen">

    <div id="start-title">
     <h1>פיצוץ אסטרואיד</h1>
    </div>
    <h3>לתחילת הלומדה לחצו על האסטרואיד</h3>

    <div id="start-button" class="animation" @click="start"></div>

   </div>
  </template>

<script>
export default {
  name: "open-screen",
  data() {
    return {
    
    };
  },
  methods: {
    start() {
        document.getElementById("start-button").classList.remove("animation");
        document.getElementById("start-button").classList.add("move-to-start");
        setTimeout(() => {
            this.$emit('next-page');
        }, 700);
  },
},
}


</script>

<style scoped>

#start-title {
    width: 90vw;
    height: 10vh;
    border-radius: 15px;
    background-color: rgb(33,84,131);
    position: absolute;
    top: 20vh;
    left: 6vw;
    text-align: center;
    box-shadow: 10px 10px 5px 0px rgba(0,0,0,0.75);
    color: white;
    line-height: 1.5rem;
}

h3 {
    color: white;
    position: absolute;
    top: 65vh;
    left: 25vw;
    font-size: small;
}


#start-button {
    width: 60vw;
    height: 28vh;
    position: absolute;
    top: 33vh;
    left: 12vw;
    background-image: url(@/assets/mymedia/burningAsteroid.png);
    background-size: 100% 100%;
    background-repeat: no-repeat;   
}

.animation {
    animation: bigAndSmallAnimation 2s ease-in-out infinite;
}

.move-to-start {
    animation: moveUpAnimation 1s ease-in-out infinite;
}

@keyframes bigAndSmallAnimation {
  0% {
    width: 60vw;
    height: 28vh;
  }

  50% {
    width: 64vw;
    height: 30vh;
  }

  100% {
    width: 60vw;
    height: 28vh;
  }
}

@keyframes moveUpAnimation {
  0% {
    transform: translateY(0);
  }

  100% {
    transform: translateY(-500px);
  }
}
</style>
