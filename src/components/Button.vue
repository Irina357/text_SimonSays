<template>
  <div>
    <h1>Simon Says</h1>
    <div class="container">
      <div class="columnLeft">
        <div v-show="activeButton" class="activeButton">
          <div class="imgContainer">
            <div class="All clBlue" v-bind:class="{opacityNone: allClass[1].opac}" @click="buttonClick(1)">
            </div>
            <div class="All clRed" v-bind:class="{opacityNone: allClass[0].opac}" @click="buttonClick(0)">
            </div>
          </div>
          <div class="imgContainer">
            <div class="All clYellow" v-bind:class="{opacityNone: allClass[3].opac}" @click="buttonClick(3)">
            </div>
            <div class="All clGreen" v-bind:class="{opacityNone: allClass[2].opac}" @click="buttonClick(2)">
            </div>
          </div>
          <div class="shadow">
          </div>
        </div>
        <div v-show="passiveButton" class="passiveButton">
          <div class="imgContainer">
            <div class="All clBlue"></div>
            <div class="All clRed"></div>
          </div>
          <div class="imgContainer">
            <div class="All clYellow"></div>
            <div class="All clGreen"></div>
          </div>
          <div class="shadow">
          </div>
        </div>
      </div>
      <div class="columnRight">
        <h2>Round: {{ round }}</h2>
        <div v-show="roundShow">
          <p>Sorry, you lost after {{ round }} rounds!</p>
        </div>
        <button class="button" @click="clickMe(time, timeAll)">Start</button>
        <h2>Game Options</h2>
        <div class="optionsContainer">
          <button @click="Normal"></button>
          <p>Normal</p>
        </div>
        <div class="optionsContainer">
          <button @click="Sound"></button>
          <p>Cound only</p>
        </div>
        <div class="optionsContainer">
          <button @click="Light"></button>
          <p>Light only</p>
        </div>
        <div class="optionsContainer">
          <button @click="FreeBoard"></button>
          <p>Free board</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data() {
    return {
      text: 'Text',
      allClass: [
        {
          opac: false
        },
        {
          opac: false
        },
        {
          opac: false
        },
        {
          opac: false
        }
      ],
      allRandom: [],
      allPlayer: [],
      time: 1500,
      timeAll: 4000,
      activeButton: false,
      passiveButton: true,
      round: 1,
      roundShow: false,
      sound: true,
      light: true,
      freeBoard: true
    }
  },
  methods: {
    Sound () {
      this.light = !this.light
      this.sound = true
      this.freeBoard = true
    },
    Light () {
      this.sound = !this.sound
      this.light = true
      this.freeBoard = true
    },
    EreeBoard () {
      this.freeBoard = !this.freeBoard
      this.light = true
      this.sound = true
    },
    Normal () {
      this.light = true
      this.sound = true
    },
    buttonClick(a) {
      this.allPlayer.push(a)
        this.allClass[a].opac = !this.allClass[a].opac
        setTimeout(() => this.allClass[a].opac = false, 300)
      if (this.sound) {
        if (a == 0) {
          const audio = new Audio(require('./glass_ping-Go445-1207030150.mp3'))
          audio.play();
        }
        if (a == 1) {
          const audio = new Audio('http://soundbible.com/mp3/Air Plane Ding-SoundBible.com-496729130.mp3');
          audio.play();
        }
        if (a == 2) {
          const audio = new Audio('http://soundbible.com/mp3/Elevator Ding-SoundBible.com-685385892.mp3');
          audio.play();
        }
        if (a == 3) {
          const audio = new Audio(require('./glass_ping-Go445-1207030150.mp3'))
          audio.play();
        }
      }
    },
    clickMe(time, timeAll) {
      this.allRandom = []
      this.allPlayer = []
      this.activeButton = !this.activeButton
      this.passiveButton = !this.passiveButton
      if (this.roundShow == true) {
        this.roundShow = !this.roundShow
      }
      let timerId = setInterval(() => {
        let rand = 0 + Math.random() * (4 + 0 - 0);
        let rand1 = Math.floor(rand)
        this.allRandom.push(rand1)
        this.allClass[rand1].opac = !this.allClass[rand1].opac
        if (rand1 == 0) {
          const audio = new Audio(require('./glass_ping-Go445-1207030150.mp3'))
          audio.play();
        }
        if (rand1 == 1) {
          const audio = new Audio('http://soundbible.com/mp3/Air Plane Ding-SoundBible.com-496729130.mp3');
          audio.play();
        }
        if (rand1 == 2) {
          const audio = new Audio('http://soundbible.com/mp3/Elevator Ding-SoundBible.com-685385892.mp3');
          audio.play();
        }
        if (rand1 == 3) {
          const audio = new Audio(require('./glass_ping-Go445-1207030150.mp3'))
          audio.play();
        }
        setTimeout(() => this.allClass[rand1].opac = false, 300)
      }, 1500)
      setTimeout(() => {
        clearInterval(timerId);
        //alert('stop');
      }, time);
      setTimeout(() => {
        if (JSON.stringify(this.allRandom) === JSON.stringify(this.allPlayer)) {
          this.activeButton = !this.activeButton
          this.passiveButton = !this.passiveButton
          this.round++
          time = time + 1500
          timeAll = timeAll + 2500
          this.clickMe(time, timeAll)
        } else {
          //alert('noy')
          this.roundShow = !this.roundShow
          this.activeButton = !this.activeButton
          this.passiveButton = !this.passiveButton
          setTimeout(() => {
            this.round = 1, this.roundShow = false
          }, 3000)
        }
      }, timeAll)
    },
    playSound(sound) {
      if (sound) {
        var audio = new Audio(sound);
        audio.play();
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="sass">
@import '../Style/StyleAll'
h1
  margin-bottom: 70px

.container, .imgContainer
  display: flex
  justify-content: center

.imgContainer
  position: relative
  z-index: 100

.columnLeft, .columnRight
  width: 300px

.columnRight
  text-align: left
  padding-left: 60px
  padding-top: 40px

.All
  width: 100px
  height: 100px
  opacity: .4

.clRed
  background: red
  border-top-right-radius: 360%



.clBlue
  background: blue
  border-top-left-radius: 360%


.clGreen
  background: green
  border-bottom-right-radius: 360%

.clYellow
  background: yellow
  border-bottom-left-radius: 360%

.opacityNone
  opacity: 1

.passiveButton, .activeButton
  position: relative

.shadow
  position: absolute
  top: 0
  left: 52px
  box-shadow: 5px 5px 5px gainsboro
  width: 203px
  height: 203px
  border-radius: 50%
  background: white

.button
  width: 100px
  height: 35px
  margin-top: 30px
  margin-bottom: 30px
  border-radius: 5px
  background: cornflowerblue
  border: none
  outline: none
  box-shadow: 3px 3px 5px gainsboro

.optionsContainer
  display: flex
</style>
