<template>
    <div id="asteroid-types">

    <div id="title-container">
    <div id="types-title">
     <h1> סוגי אסטרואידים </h1>
     
    </div>
    <h3> לחצו על כל אסטרואיד כדי לגלות את סוגו </h3>
    </div>

    <div v-for="num in 3" :key="num - 1" :id="num - 1" @click="openType" :class="[showType ? '' : 'animation', `asteroid${num - 1}`, (num - 1) === Number(asteroidType) ? 'high-z-index': '']" ></div>

    <type-info v-if="showType" :asteroidType = "asteroidType" @close-type="closeType"></type-info>

    <div id="next-button" v-if="visited.length === 3" @click="next">המשך</div>

   </div>
  </template>


<script>
import typeInfo from './typeInfo.vue';

export default {
  name: "asteroid-types",
    components: {
        typeInfo,
    },

  data() {
    return {
        showType: false,
        asteroidType: '',
        btnClick: 0,
        visited: []
    };
  },
  methods: {
    openType(event) {
        this.asteroidType = event.target.id; 
        // event.target.id.classList.add("")
        this.btnClick++;
        this.showType = !this.showType;
        if(!this.visited.includes(event.target.id)) {
            this.visited.push(event.target.id);
        }
        
    },

    closeType() {
        this.showType = false;
    },

    next() {
        document.getElementById("next-button").classList.add("on-click-animation")
        setTimeout(() => {
            this.$emit('next-page');
        }, 700);
    },
  },
};

</script>

<style scoped>
#title-container {
    display: flex;
    flex-direction: column;
    align-items: flex-end;
    position: absolute;
    top: 14vh;
    left: 26vw;
}

#types-title {
    width: 85vw;
    height: 8vh;
    border-radius: 15px;
    background-color: rgb(33 84 131 / 82%);
    /* position: absolute; */
    /* top: 14vh;
    left: 26vw; */
    box-shadow: 10px 10px 5px 0px rgba(0,0,0,0.75);
    color: white;
    display: flex;
    justify-content: center;
    align-items: center;
}

h3 {
    color: white;
    font-size: medium;
    padding-right: 15%;
    font-family: assistantLight;
    margin-top: 4%;
    margin-bottom: 0;
}

.asteroid0 {
    animation-duration: 1.5s;
    width: 40%;
    height: 20%;
    background-image: url(@/assets/mymedia/babyAsteroid.png);
    background-repeat: no-repeat;
    background-size: 100% 100%;
    position: absolute;
    top: 27%;
    right: 1%;
    /* animation: floatAnimation 1.5s ease-in-out infinite; */
}

.animation {
    animation-name: floatAnimation;
    animation-timing-function: ease-in-out;
    animation-iteration-count: infinite;
}

.asteroid1 {
    width: 60%;
    height: 30%;
    background-image: url(@/assets/mymedia/teenAsteroid.png);
    background-repeat: no-repeat;
    background-size: 100% 100%;
    position: absolute;
    top: 33%;
    animation-duration: 2s;
    animation-direction: reverse;
}

.asteroid2 {
  width: 61%;
    height: 35%;
    background-image: url(@/assets/mymedia/adultAsteroid.png);
    background-repeat: no-repeat;
    background-size: 100% 100%;
    position: absolute;
    top: 55%;
    right: -2%;
    animation-duration: 3s;
}

@keyframes floatAnimation {
  0% {
    transform: translateY(0);
  }

  50% {
    transform: translateY(-10px);
  }

  100% {
    transform: translateY(0);
  }
}

#next-button {
    width: 17%;
    height: 5%;
    background-color: rgb(146,146,146);
    box-shadow: 10px 10px 5px 0px rgba(0,0,0,0.75);
    border-radius: 10px;
    color: white;
    line-height: 2rem;
    text-align: center;
    font-size: large;
    position: absolute;
    top: 83%;
    left: 2%;
}

.high-z-index {
    z-index: 10;
}

.on-click-animation {
    animation: upAnimation 0.5s ease-in-out;
}

@keyframes upAnimation {
  0% {
    transform: translateY(0);
  }

  50% {
    transform: translateY(-5px);
  }

  100% {
    transform: translateY(0);
  }
}

</style>
