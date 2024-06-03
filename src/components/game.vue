
<template>
    <div id="game" @touchstart="startMove" @touchend="stopMove" @touchmove.prevent="moveShip">
        <div id="ship" :style="{ left: shipPosition.x + 'px', top: shipPosition.y + 'px' }"></div>
        <div v-for="(asteroid, index) in asteroids" :key="index" class="asteroid"
            :style="{ left: asteroid.x + 'px', top: asteroid.y + 'px' }"></div>

        <div id="explosion" v-if="explosion"></div>
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
            shipPosition: { x: 250, y: 400 },
            asteroids: [],
            gameInterval: null,
            score: 0,
            movingLeft: false,
            movingRight: false,
            explosion:false,
            gameOverMessage: false,
            
        };
    },
    created() {
        this.startGame();
        
    },
    methods: {
        startGame() {
            this.explosion = false;
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
                if (asteroid.y > 500) {
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
            this.explosion = true;
            // this.document.getElementById('ship').style.backgroundImage = "url('src/assets/mymedia/giphy.gif')";

            setTimeout(()=> {
                this.explosion = false;
                this.gameOverMessage = true;
            }, 1200);
            // this.gameOverMessage = true;
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
    background-image: url(@/assets/mymedia/spaceShip.png);
    background-repeat: no-repeat;
    background-size: 100% 100%;
    transition: left 0.2s;
}

.asteroid {
    width: 50px;
    height: 50px;
    position: absolute;
    background-image: url(@/assets/mymedia/babyAsteroid.png);
    background-repeat: no-repeat;
    background-size: 100% 100%;
}

#explosion {
    width: 100vw;
    height: 80vh;
    background-image: url(@/assets/mymedia/giphy.gif);
    background-repeat: no-repeat;
    background-size: 100% 100%;
    z-index: 5;
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

button {
    border: none;
    box-shadow: 5px 5px 5px 0px rgba(0, 0, 0, 0.75);
    border-radius: 4px;
    height: 10%;
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
  

   
   

   <!-- <template>
    <div id="game">
      
    
        <div class="grid-container">
  <div>1</div>
  <div>2</div>
  <div>3</div>  
  <div>4</div>
  <div>5</div>
  <div>6</div>  
  <div>7</div>
  <div>8</div>
  <div>9</div>
  <div>10</div>
  <div>11</div>
  <div>12</div>
  <div>13</div>
  <div>14</div>
  <div>15</div>
  <div>16</div>
        </div>
      

        <div id="next-button" v-if="gameOverMessage" @click="next">לסיום הלומדה</div>
    </div>
  </template>


<script>
export default {
    name: "game",
    data() {
        return {
            gameOverMessage:true,
           
        };
    },
  
    methods: {




        next() {
            document.getElementById("next-button").classList.add("on-click-animation");
            setTimeout(() => {
                this.$emit('next-page');
            }, 700);
        }
    },
}

    </script>

  <style scoped>

  #game {
    width:100vw;
    height: 100vh;
  }

  .grid-container {
    
  display: grid;
  grid-template-columns: 25% 25% 25% 25%;
  gap: 5%;
  padding: 10%;
  justify-content: center;
  margin-top: 15%;
}

.grid-container > div {
  background-color: rgba(255, 255, 255, 0.8);
  text-align: center;
  padding: 20px 0;
  font-size: 30px;
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
    top: 80%;
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



<!-- 
  <template>
    <div id="app">
      <div class="grid">
        <div v-for="row in gridRows" :key="row" class="row">
          <div v-for="col in gridCols" :key="col" class="cell" ></div>
        </div>

        <div class="player"></div>
      
      <div id="next-button" v-if="gameOverMessage" @click="next">לסיום הלומדה</div>
    </div>
    </div>
  </template>
  
  <script>
  export default {
    name: "game",
    data() {
      return {
        gridRows: 8,
        gridCols: 7,
        
        gameOverMessage: true,
      };
    },
    methods: {
      
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
  .grid {
    display: grid;
    grid-template-columns: repeat(7, 50px);
    grid-template-rows: repeat(8, 50px);
    gap: 1%;
    justify-content: center;
    margin-top: 15%;
  }
  
  .cell {
    border: 1px solid black;
  }
  
  .asteroid {
    background-image: url('@/assets/mymedia/babyAsteroid.png');
    background-size: cover;
    width: 50px;
    height: 50px;
  }
  
  .explosion {
    background-image: url('@/assets/mymedia/burningAsteroid.png');
    background-size: cover;
    width: 50px;
    height: 50px;
  }
  
  .player {
    background-image: url('@/assets/mymedia/spaceShip.png');
    background-size: cover;
    width: 50px;
    height: 50px;
    
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
    top: 80%;
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
  
  
