<template>
    <div id="end-screen">

        <div class="endmessage">
            <h1>כל הכבוד!!
                <br>
                סיימת את הלומדה
            </h1>

            <h1>
                בהצלחה בהמשך פיצוץ האסטרואידים!
            </h1>

        </div>

        <div id="go-to-start"  @click="toStart">לתחילת הלומדה</div>

        <img class="asteroid0 animation" src="@/assets/mymedia/babyAsteroid.png" alt="asteroid0">
        <img class="asteroid1 animation" src="@/assets/mymedia/teenAsteroid.png" alt="asteroid1">
        <img class="asteroid2 animation" src="@/assets/mymedia/adultAsteroid.png" alt="asteroid2">



    </div>
</template>

<script>
export default {
    name: "end-screen",
    data() {
        return {

        };
    },
    methods: {
        toStart() {
            this.$emit('to-start');
        },
    },
}


</script>

<style scoped>
#end-screen {
    display: flex;
    justify-content: center;
    align-items: stretch;
    flex-direction: column;
}

.endmessage {
    direction: rtl;
    color: white;
    text-shadow: 4px 3px #000000;
    text-align: center;
    margin-top: 30%;
    z-index: 2;
    line-height: 3rem;
}

h1 {
    padding: 10%;
}

.asteroid0 {
    animation-duration: 1.5s;
    width: 45%;
    height: auto;
    position: absolute;
    top: 10%;
    left: 10%;

}

.asteroid1 {
    width: 70%;
    height: auto;
    position: absolute;
    top: 28%;
    right: -25%;
    animation-duration: 2s;
    animation-direction: reverse;
}

.asteroid2 {
    width: 80%;
    height: auto;
    position: absolute;
    top: 50%;
    left: -20%;
    animation-duration: 3s;
}

.animation {
    animation-name: floatAnimation;
    animation-timing-function: ease-in-out;
    animation-iteration-count: infinite;

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

#go-to-start {
    width: 40%;
    height: 5%;
    background-color: rgb(197, 90, 17);
    box-shadow: 10px 10px 5px 0px rgba(0, 0, 0, 0.75);
    border-radius: 10px;
    color: white;
    line-height: 2rem;
    text-align: center;
    font-size: large;
    position: absolute;
    top: 90%;
    left: 28%;
    z-index: 4;
}
</style>
