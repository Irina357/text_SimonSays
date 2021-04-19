<template>
  <div>
    <button type="button" class="button" @click="clickMe()">{{text}}</button>
  </div>
</template>
<script>
export default {
  props: ['text'],
  data () {
    return {
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
      roundShow: false
    }
  },
  methods: {
     clickMe() {
       this.$emit('clickMe', {
        allClass: this.allClass,
         allRandom: this.allRandom,
         allPlayer: this.allPlayer,
      time: this.time,
      timeAll: this.timeAll,
      activeButton: this.activeButton,
      passiveButton: this.passiveButton,
      round: this.round,
      roundShow: this.roundShow
       }
       )
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
      }, this.time);
      setTimeout(() => {
        if (JSON.stringify(this.allRandom) === JSON.stringify(this.allPlayer)) {
          this.activeButton = !this.activeButton
          this.passiveButton = !this.passiveButton
          this.round++
          this.time = this.time + 1500
          this.timeAll = this.timeAll + 2500
          this.clickMe(this.time, this.timeAll)
        } else {
          //alert('noy')
          this.roundShow = !this.roundShow
          this.activeButton = !this.activeButton
          this.passiveButton = !this.passiveButton
          setTimeout(() => {
            this.round = 1, this.roundShow = false
          }, 3000)
        }
      }, this.timeAll)
    }
  }
}
</script>
<style lang="sass">
.button
  width: 70px
  height: 35px
  background: aquamarine

</style>
