<template>

  <div id="transperant-background">
    <div id="asteroid-type" 
    :class="{
      'baby': asteroidType === 0,
      'teen': asteroidType === 1,
      'adult': asteroidType === 2
    }">

      <div class="textInfoAsteroid">
            <h1 class="typeTitle"> {{ asteroidTypeInfo[asteroidType].title }} </h1>
            <p class="infoText"> {{ asteroidTypeInfo[asteroidType].text }} </p>
        </div>



        
    </div>
    </div>
</template>

<script>
export default {
  name: "type-info",
  props: ['asteroidType'],
  data() {
    return {
      asteroidTypeInfo: [
                {
                  title: 'אסטרואיד בייבי',
                  text: 'אסטרואיד ממש קטן והורס רק שכונות מקומיות'
                },
                {
                    title: 'אסטרואיד נער מתבגר',
                    text: 'אסטרואיד שהוא די חרא כי הוא בכוונה מנסה להפציץ מקומות שהוא לא אוהב '
                },
                {
                    title: 'אסטרואיד בוגר',
                    text: 'אסטרואיד ממש גדול שיכול להשמיד את כדור הארץ'
                }
            ]
    
    };
  },
  methods: {
 
},
}
</script>

<style scoped>

#transperant-background {
  width: 100vw;
  height: 90vh;
  background-color: rgba(255, 255, 255, 0.644);
  z-index: 3;
  position: relative;
}

#asteroid-type {
  width: 70%;
  height: 30%;
  box-shadow: 10px 10px 5px 0px rgba(0,0,0,0.75);
  border-radius: 15px;
  color: black;
  text-align: center;
  background-color: rgb(222,235,247);
  position: absolute;
  line-height: 2rem;
  padding-top: 15%;
}

.baby {
  top: 35%;
  left: 10%;
}


</style>
