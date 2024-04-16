<!-- <template>
    <div id="game">




        <div id="next-button" @click="next">לסיום הלומדה</div>

    </div>
</template>

<script>
export default {
    name: "game",
    data() {
        return {
           
        };
    },
    methods: {
        

        next() {
            document.getElementById("next-button").classList.add("on-click-animation");
            setTimeout(() => {
                this.$emit('next-page');
            }, 700);
        },
    },
};
</script>

<style scoped>



#next-button {
    width: 40%;
    height: 5%;
    background-color: rgb(197,90,17);
    box-shadow: 10px 10px 5px 0px rgba(0,0,0,0.75);
    border-radius: 10px;
    color: white;
    line-height: 2rem;
    text-align: center;
    font-size: large;
    position: absolute;
    top: 83%;
    left: 25%;
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

</style>  -->


<!-- <template>
    <div id="game">
        <div id="game-container" v-for="(card, index) in cards" :key="index" @click="flipCard(index)" class="card" :class="{ flipped: card.flipped }">
            <span v-if="card.flipped">{{ card.value }}</span>
        </div>
        <div id="next-button" @click="next">לסיום הלומדה</div>
    </div>
</template>

<script>
export default {
    name: "game",
    data() {
        return {
            cards: [
                { value: 'A', flipped: false },
                { value: 'B', flipped: false },
                { value: 'C', flipped: false },
                // { value: 'D', flipped: false },
                { value: 'A', flipped: false },
                { value: 'B', flipped: false },
                { value: 'C', flipped: false },
                // { value: 'D', flipped: false },
            ],
            flippedCards: []
        };
    },
    methods: {
        flipCard(index) {
            if (this.flippedCards.length < 2 && !this.cards[index].flipped) {
                this.cards[index].flipped = true;
                this.flippedCards.push(index);

                if (this.flippedCards.length === 2) {
                    const [firstIndex, secondIndex] = this.flippedCards;
                    if (this.cards[firstIndex].value !== this.cards[secondIndex].value) {
                        setTimeout(() => {
                            this.cards[firstIndex].flipped = false;
                            this.cards[secondIndex].flipped = false;
                            this.flippedCards = [];
                        }, 1000);
                    } else {
                        this.flippedCards = [];
                    }
                }
            }
        },
        next() {
            document.getElementById("next-button").classList.add("on-click-animation");
            setTimeout(() => {
                this.$emit('next-page');
            }, 700);
        }
    }
};
</script>

<style scoped>
#game {
    margin-top: 30%;
    margin-left: 5%;
}

.card {
    width: 100px;
    height: 100px;
    background-color: lightblue;
    margin: 5px;
    display: inline-flex;
    justify-content: center;
    align-items: center;
    cursor: pointer;
}

.flipped {
    background-color: #fff;
}

#next-button {
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
    top: 83%;
    left: 25%;
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
</style> -->

<template>
    <div id="game" @touchstart="startMove" @touchend="stopMove" @touchmove.prevent="moveShip">
        <div id="ship" :style="{ left: shipPosition.x + 'px', top: shipPosition.y + 'px' }"></div>
        <div v-for="(asteroid, index) in asteroids" :key="index" class="asteroid"
            :style="{ left: asteroid.x + 'px', top: asteroid.y + 'px' }"></div>

        <div id="message" v-if="gameOverMessage"> {{ `Game Over! Your score: ${this.score}` }} 
        <button @click="startGame">שחק שוב</button>
        </div>
        <div id="next-button" v-if="gameOverMessage" @click="next">לסיום הלומדה</div>
    </div>
</template>

<script>
export default {
    name: "game",
    data() {
        return {
            shipPosition: { x: 250, y: 350 },
            asteroids: [],
            gameInterval: null,
            score: 0,
            movingLeft: false,
            movingRight: false,
            gameOverMessage: false,
        };
    },
    created() {
        this.startGame();
        
    },
    methods: {
        startGame() {
            this.gameOverMessage = false;
            this.score = 0;
            this.gameInterval = setInterval(() => {
                this.moveAsteroids();
                this.checkCollision();
            }, 100);
        },
        moveAsteroids() {
            this.asteroids.forEach(asteroid => {
                asteroid.y += 5;
                if (asteroid.y > 400) {
                    this.removeAsteroid(asteroid);
                    this.score += 10;
                }
            });
            if (Math.random() < 0.05) {
                this.createAsteroid();
            }
        },
        createAsteroid() {
            const asteroid = { x: Math.random() * 500, y: 0 };
            this.asteroids.push(asteroid);
        },
        removeAsteroid(asteroid) {
            const index = this.asteroids.indexOf(asteroid);
            this.asteroids.splice(index, 1);
        },
        checkCollision() {
            const shipRect = document.getElementById('ship').getBoundingClientRect();
            this.asteroids.forEach(asteroid => {
                const asteroidRect = {
                    left: asteroid.x,
                    top: asteroid.y,
                    right: asteroid.x + 50,
                    bottom: asteroid.y + 50
                };
                if (
                    shipRect.right >= asteroidRect.left &&
                    shipRect.left <= asteroidRect.right &&
                    shipRect.bottom >= asteroidRect.top &&
                    shipRect.top <= asteroidRect.bottom
                ) {
                    this.gameOver();
                }
            });
        },
        gameOver() {
            clearInterval(this.gameInterval);
            this.gameOverMessage = true;
            this.asteroids = [];
            this.shipPosition = { x: 250, y: 350 };
            this.asteroids = [];
            this.gameInterval = null;
            this.movingLeft = false;
            this.movingRight = false;
        
        },
        startMove(event) {
            const touchX = event.touches[0].clientX;
            if (touchX < window.innerWidth / 2) {
                this.movingLeft = true;
            } else {
                this.movingRight = true;
            }
        },
        stopMove() {
            this.movingLeft = false;
            this.movingRight = false;
        },
        moveShip(event) {
            const touchX = event.touches[0].clientX;
            const deltaX = touchX - this.shipPosition.x;
            const newPositionX = this.shipPosition.x + deltaX;

            // Ensure the ship stays within the game area
            this.shipPosition.x = Math.max(0, Math.min(window.innerWidth - 50, newPositionX));
        },

        next() {
            document.getElementById("next-button").classList.add("on-click-animation");
            setTimeout(() => {
                this.$emit('next-page');
            }, 700);
        }
    }
};
</script>

<style scoped>
#game {
    width: 100%;
    height: 100vh;
    position: relative;
    overflow: hidden;
}

#ship {
    width: 50px;
    height: 50px;
    position: absolute;
    background-image: url(src/assets/mymedia/spaceShip.png);
    background-repeat: no-repeat;
    background-size: 100% 100%;
    transition: left 0.2s;
}

.asteroid {
    width: 50px;
    height: 50px;
    position: absolute;
    background-image: url(src/assets/mymedia/burningAsteroid.png);
    background-repeat: no-repeat;
    background-size: 100% 100%;
}

#message {
    width: 55%;
    height: 30%;
    background-color: rgb(200, 215, 248);
    color: black;
    position: absolute;
    top: 25%;
    left: 20%;
    line-height: 5rem;
    text-align: center;
    font-size: x-large;
    box-shadow: 10px 10px 5px 0px rgba(0, 0, 0, 0.75);
    border-radius: 10px;
    display: flex;
    flex-direction: column;
    align-items: center;
}

#next-button {
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
    top: 75%;
    left: 25%;
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
