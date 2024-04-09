<template>
    <div id="asteroid-types">

    <div id="title-container">
    <div id="types-title">
     <h1> סוגי אסטרואידים </h1>
     
    </div>
    <h3> לחצו על כל אסטרואיד כדי לגלות את סוגו </h3>
    </div>
]
    
    <div id="baby-asteroid" @click="openType" :class="{'animation': !showType}"></div>
    <div id="teen-asteroid" @click="openType" :class="{'animation': !showType}"></div>
    <div id="adult-asteroid" @click="openType" :class="{'animation': !showType}"></div>

    <type-info v-if="showType" :asteroidType = "asteroidType"></type-info>

    <div id="next-button" v-if="btnClick >= 3 && !showInfo" @click="next">המשך</div>

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
    };
  },
  methods: {
    openType(event) {


        if(event.target.id === "baby-asteroid") {
            this.asteroidType = 0;
            this.btnClick++;
        } else if(event.target.id === "teen-asteroid"){
            this.asteroidType = 1;
            this.btnClick++;
        } else if(event.target.id === "adult-asteroid"){
            this.asteroidType = 2;
            this.btnClick++;
        }
        this.showType = true;
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
    background-color: rgb(33,84,131);
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

#baby-asteroid {
    width: 45%;
    height: 20%;
    background-image: url(src/assets/mymedia/babyAsteroid.png);
    background-repeat: no-repeat;
    background-size: 100% 100%;
    position: absolute;
    top: 27%;
    right: 1%;
    animation: floatAnimation 1.5s ease-in-out infinite;
}

/* .animation {
    animation: floatAnimation 1.5s ease-in-out infinite;
} */

#teen-asteroid {
    width: 65%;
    height: 30%;
    background-image: url(src/assets/mymedia/teenAsteroid.png);
    background-repeat: no-repeat;
    background-size: 100% 100%;
    position: absolute;
    top: 33%;
    /* transform: rotate(180deg); */
    animation: floatAnimation var(--duration) ease-in-out infinite reverse;
}

#adult-asteroid {
    width: 80%;
    height: 35%;
    background-image: url(src/assets/mymedia/adultAsteroid.png);
    background-repeat: no-repeat;
    background-size: 100% 100%;
    position: absolute;
    top: 55%;
    right: 0%;
    animation: floatAnimation 3s ease-in-out infinite;
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
    line-height: 2.5rem;
    text-align: center;
    font-size: large;
    position: absolute;
    top: 83%;
    left: 2%;
}

</style>
