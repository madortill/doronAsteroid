<template>
    <div id="asteroid-explosion">

        <div id="explosion-title">
            <h1>?איך מפוצצים אסטרואיד</h1>

        </div>


        <div class="callout" @click="onClick">
            <div class="flip-card flip-card--click" :class="{ 'flip': isFlipped }">
                <div class="front">
                    <div class="box">

                        תחנת השיגור היא האחראית לחישוב הקורדינאטות שבהן האסטרואיד נמצא בכל רגע נתון.
                        תפקידכם הוא לכוון את משגר הפצצות לכיוון האסטרואיד לפי הקורדינאטות שקיבלתם מתחנת השיגור.

                    </div>
                </div>
                <div class="back">
                    <div class="box instructions">

                        במשחק הבא עליכם להתחמק מהאסטרואידים הבוערים שמגיעים לכיוון ספינת החלל שלכם.
                        על מנת להימנע מהאסטרואידים המרושעים עליכם לגרור את ספינת החלל למקום בטוח. עבור כל אסטרואיד שתימנעו ממנו תצברו 10 נקודות, אך אם אסטרואיד יפגע בכם - תיפסלו.
                        בהצלחה!

                    </div>
                </div>
            </div>
        </div>

        <img id="burningAsteroidGraphic"  src="@/assets/mymedia/burningAsteroid.png" alt="graphic" >

        <h4> הקליקו על הכרטיס כדי להפוך אותו </h4>

        <div v-if="isFlipped" id="go-to-game-button" @click="next">!למשחק</div>
    </div>
</template>

<script>
export default {
    name: "asteroid-explosion",
    data() {
        return {
            isFlipped: false
        };
    },
    methods: {
        onClick() {
            this.isFlipped = !this.isFlipped;
        },

        next() {
            document.getElementById("go-to-game-button").classList.add("on-click-animation");
            setTimeout(() => {
                this.$emit('next-page');
            }, 700);
        },
    },
};
</script>

<style scoped>
#explosion-title {
    width: 90vw;
    height: 8vh;
    border-radius: 15px;
    background-color: rgb(33, 84, 131);
    position: absolute;
    top: 14vh;
    left: 12vw;
    box-shadow: 10px 10px 5px 0px rgba(0, 0, 0, 0.75);
    color: white;
    display: flex;
    justify-content: center;
    align-items: center;
}

.flip-card {
    width: 278px;
    height: 335px;
    position: absolute;
    perspective: 600px;
    top: 25%;
    left: 5%;
}

.front {
    position: absolute;
    top: 0;
    left: 0;
    z-index: 900;
    width: inherit;
    height: inherit;
    transform: rotateX(0deg) rotateY(0deg);
    transform-style: preserve-3d;
    backface-visibility: hidden;
    transition: all .4s ease-in-out;
}

.back {
    float: none;
    position: absolute;
    top: 0;
    left: 0;
    z-index: 800;
    width: inherit;
    height: inherit;
    transform: rotateY(-179deg);
    transform-style: preserve-3d;
    backface-visibility: hidden;
    transition: all .4s ease-in-out;


}

.flip-card--x .front {
    transform: rotateX(0deg) rotateY(0deg);
}

.back {
    transform: rotateX(-179deg);
}

.flip-card--x.flip .front {
    transform: rotateX(180deg);
}

.back {
    transform: rotateX(0deg) rotateY(0deg);
}


.flip .front {
    transform: rotateY(180deg);
}

.back {
    transform: rotateX(0deg) rotateY(0deg);
}



.callout {
    margin: 20px auto;
    width: 278px;
}

.callout .box {
    background-color: #f6f6f6;
    border: 1px solid #ccd9e8;
    background-clip: padding-box;
    height: 90%;
    width: 80%;
    padding: 20px;
    border-radius: 15px;
    text-align: center;
    direction: rtl;
    line-height: 3rem;
    padding-top: 10%;
}

.instructions {
    line-height: 2rem !important; 
}


.callout .back .box {
    background-color: #0b417c;
    border-color: #0b417c;
    color: #fff;
}

#burningAsteroidGraphic {
    width: 60%;
    height: auto;
    position: absolute;
    top: 55%;
    right: -10%;
    transform: scaleX(-1) rotate(0.09turn);
}


h4 {
    color: white;
    font-family: assistantLight;
    font-size: small;
    position: absolute;
    top: 75%;
    left: 15%;
}


#go-to-game-button {
    width: 20%;
    height: 5%;
    background-color: rgb(216,90,35);
    box-shadow: 10px 10px 5px 0px rgba(0, 0, 0, 0.75);
    border-radius: 25px;
    color: white;
    line-height: 2rem;
    text-align: center;
    font-size: large;
    position: absolute;
    top: 82%;
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
</style>