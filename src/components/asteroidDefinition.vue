<template>
    <div id="asteroid-definition">

    <div id="definition-title">
     <h1> ?מהו אסטרואיד </h1>
    </div>

    <!-- <div id="asteroid-graphic"></div> -->
    <img id="asteroid-graphic" src="src/assets/mymedia/asteroid.png" alt="graphic" >
    <div id="explanation">אסטרואיד הוא יצור מרושע שמטרתו להשמיד את כדור הארץ ואנחנו בברוגז איתו ממש. 
        הוא נראה כמו כדור עגול כזה אבל לא חלק כי יש לו בליטות מכוערות שנראות כמו חצ׳קונים.
</div>

    <div id="next-button" @click="next">המשך</div>

   </div>
  </template>

<script>
export default {
  name: "asteroid-definition",
  data() {
    return {
    
    };
  },
  methods: {
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

#definition-title {
    width: 90vw;
    height: 8vh;
    border-radius: 15px;
    background-color: rgb(33,84,131);
    position: absolute;
    top: 14vh;
    left: 26vw;
    box-shadow: 10px 10px 5px 0px rgba(0,0,0,0.75);
    color: white;
    display: flex;
    justify-content: center;
    align-items: center;
}

#asteroid-graphic {
    width: 60%;
    height: auto;
    background-image: url(src/assets/mymedia/asteroid.png);
    background-repeat: no-repeat;
    background-size: 100% 100%;
    position: absolute;
    top: 23%;
    right: 1%;
    animation-name: spin;
    animation-duration: 5000ms;
    animation-iteration-count: infinite;
    animation-timing-function: linear;  
}

#explanation {
    direction: rtl;
    position: absolute;
    background-color: rgb(118,113,113);
    box-shadow: 10px 10px 5px 0px rgba(0,0,0,0.75);
    border-radius: 15px;
    width: 67%;
    height: 40%;
    top: 40%;
    right: 30%;
    color: white;
    font-size: large;
    text-align: center;
    padding-top: 20%;
    padding-left: 5%;
    padding-right: 5%;
    z-index: -2;
    box-sizing: border-box;
    line-height: 130%;
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

@keyframes spin {
    from {
        transform:rotate(0deg);
    }
    to {
        transform:rotate(360deg);
    }
}

@keyframes bigAndSmallAnimation {
  0% {
    width: 70%;
    height: 32%;
  }

  50% {
    width: 74vw;
    height: 34vh;
  }

  100% {
    width: 70%;
    height: 32%;
  }
}

</style>