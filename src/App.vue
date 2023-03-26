<template>
  <div style="margin-top: 10vh;">

    <h1>Online Timer</h1>
    
    <h3>Time left:</h3>
    <h2 style="color: timeColor">{{ displayClock }}</h2>
    

    <h3 hidden>Times up.</h3>

    <button v-if="paused == true && timer > 0" @click="paused = false, startTimer()">Start</button>
    <button v-else-if="paused == false && timer > 0" @click="pauseTimer">Pause</button>
    <button v-else disabled>Start</button>

    <br>
    <br>

    <button @click="showControls = !showControls">Show controls</button>

    <div v-if="showControls">
      <div>
        <button @click="timer++">+1s</button>
        <button @click="timer--">-1s</button>
      </div>

      <div>
        <button @click="timer+=10">+10s</button>
        <button @click="timer-=10">-10s</button>
      </div>

      <div>
        <button @click="timer+=60">+1m</button>
        <button @click="timer-=60">-1m</button>
      </div>

      <div>
        <button @click="timer+=600">+10m</button>
        <button @click="timer-=600">-10m</button>
      </div>

      <div>
        <button @click="timer+=3600">+1h</button>
        <button @click="timer-=3600">-1h</button>
      </div>

      <button @click="timer = 0">Reset to 0</button>


    </div>


    <div id="settings-icon" @click="showSettings = !showSettings">
      <svg xmlns="http://www.w3.org/2000/svg" class="icon icon-tabler icon-tabler-settings" width="32" height="32" viewBox="0 0 24 24" stroke-width="1.5" stroke="#000000" fill="none" stroke-linecap="round" stroke-linejoin="round">
      <path stroke="none" d="M0 0h24v24H0z" fill="none"/>
      <path d="M10.325 4.317c.426 -1.756 2.924 -1.756 3.35 0a1.724 1.724 0 0 0 2.573 1.066c1.543 -.94 3.31 .826 2.37 2.37a1.724 1.724 0 0 0 1.065 2.572c1.756 .426 1.756 2.924 0 3.35a1.724 1.724 0 0 0 -1.066 2.573c.94 1.543 -.826 3.31 -2.37 2.37a1.724 1.724 0 0 0 -2.572 1.065c-.426 1.756 -2.924 1.756 -3.35 0a1.724 1.724 0 0 0 -2.573 -1.066c-1.543 .94 -3.31 -.826 -2.37 -2.37a1.724 1.724 0 0 0 -1.065 -2.572c-1.756 -.426 -1.756 -2.924 0 -3.35a1.724 1.724 0 0 0 1.066 -2.573c-.94 -1.543 .826 -3.31 2.37 -2.37c1 .608 2.296 .07 2.572 -1.065z" />
      <circle cx="12" cy="12" r="3" />
      </svg>
    </div>

    <div v-if="showSettings" id="settings">
      <h2>Settings</h2>
      <p>Nothing here yet.</p>
    </div>
    


    <footer style="position: absolute; bottom: 2px; width: 100%;">
      <p @mouseover="changeHeart" style="">created with {{heart}} by Johan</p>
    </footer>

  </div>
</template>

<script>

export default {
  name: 'App',
  components: {
  },
  data(){
    return{
      timer: 2,
      heart: '❤️',
      paused: true,
      showControls: true,
      showSettings: false,
    }
  },
  methods:{
    startTimer(){
      if(this.timer > 0 && !this.paused){
        setTimeout(()=> {
          this.timer -= 0.01
          this.startTimer()
        }, 10)
      }
      if(this.timer < 0){
        this.timersOver()
      }
    },
    timersOver(){
      this.timer = 0
      this.paused = true
    },
    pauseTimer(){
      this.paused = true
    },
    changeHeart(){
      if(this.heart === '❤️'){
        this.heart = '🧡'
      }
      else if(this.heart === '🧡'){
        this.heart = '💛'
      }
      else if(this.heart === '💛'){
        this.heart = '💚'
      }
      else if(this.heart === '💚'){
        this.heart = '💙'
      }
      else if(this.heart === '💙'){
        this.heart = '💜'
      }
      else if(this.heart === '💜'){
        this.heart = '❤️'
      }
    },
    created(){
      this.startTimer()
    },
  },
  watch:{
    
  },
  computed:{
    displayClock(){
      if(this.timer < 60){
        return this.timer.toFixed(2) + 's'
      }
      else if(this.timer < 3600){
        var minutes = Math.floor(this.timer / 60)
        var seconds = this.timer % 60
        return minutes.toFixed(0) + 'm ' +  seconds.toFixed(2) + 's'
      }
      else{
        var hours = Math.floor(this.timer / 60 / 60)
        var hminutes = Math.floor(this.timer / 60 % 60)
        var hseconds = this.timer % 60
        return hours.toFixed(0) + 'h ' + hminutes.toFixed(0) + 'm ' +  hseconds.toFixed(2) + 's'
      }
      
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #000000;
  margin-top: 60px;
}

#settings-icon{
  position: absolute;
  left: 10px;
  top: 10px;
}

#settings{
  border-radius: 20px;
  border: 5px solid;
  background-color: white;
  position: absolute;
  left: 20%;
  top: 30%;
  box-shadow: 2px black;
  width: 60%;
  height: 40%;
}
</style>
