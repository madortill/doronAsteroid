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

        <img class="asteroid0" src="src/assets/mymedia/babyAsteroid.png" alt="asteroid0" >
        <img class="asteroid1" src="src/assets/mymedia/teenAsteroid.png" alt="asteroid1" >
        <img class="asteroid2" src="src/assets/mymedia/adultAsteroid.png" alt="asteroid2" >



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
    /* text-shadow: 10px 10px 5px 0px rgba(0, 0, 0, 0.75); */
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
    /* animation-duration: 1.5s; */
    width: 45%;
    height: auto;
    position: absolute;
    top: 15%;
    left: 10%;
    /* animation: floatAnimation 1.5s ease-in-out infinite; */
}

.asteroid1 {
    width: 70%;
    height: auto;
    position: absolute;
    top: 33%;
    right: -25%;
    /* animation-duration: 2s; */
    /* animation-direction: reverse; */
}

.asteroid2 {
    width: 80%;
    height: auto;
    position: absolute;
    top: 55%;
    left: -20%;
    /* animation-duration: 3s; */
}
</style>
