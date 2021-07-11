<template>
  <div id="app">
    <img src="./assets/cronometro.png" class="img" />
    <a class="timer">{{ number }}</a>

    <div class="area-btn">
      <button class="button"  @click="go">{{ btnText }}</button>
      <button class="button" @click="clear">LIMPAR</button>
    </div>

    <div v-show="history.length" class="list">
      <ul>
        <li 
          v-for="(item, i) in history" 
          :key="i">
          VOCÊ FEZ UMA PAUSA DE: {{ item }}
        </li>
      </ul>

      <button 
        @click="history = []">
        Limpar histórico
      </button>
    </div>
  </div>
</template>

<script>

export default {
  name: 'App',

  data() {
    return {
      number: 0,
      btnText: 'VAI',
      timer: null,
      seconds: 0,
      minutes: 0,
      hours: 0,
      history: []
    }
  },

  methods: {
    go() {
      if(this.timer !== null) {
        clearInterval(this.timer)
        this.timer = null
        this.btnText = 'VAI'
        if(this.seconds !== 0) this.history.push(this.number)
        
      } else {
        this.timer = setInterval(() => {
          this.runTimer()
        }, 100)
        this.btnText = 'PAUSAR'
      }
    },

    clear() {
      if(this.timer !== null) {
        clearInterval(this.timer)
        this.timer = null
      }
      this.seconds = 0
      this.minutes = 0
      this.hours = 0
      this.number = 0
      this.btnText = 'VAI'
      this.history = []
    },
  
    runTimer() {
      this.seconds++

      if(this.seconds == 59) {
        this.seconds = 0
        this.minutes++
      }

      if(this.minutes == 59) {
        this.minutes = 0
        this.hours++
      }

      let format = (this.hours < 10 ? '0'+this.hours : this.hours) + ':'
      + (this.minutes < 10 ? '0'+this.minutes : this.minutes) + ':'
      + (this.seconds < 10 ? '0'+this.seconds : this.seconds)

      return this.number = format
    }
  } 
}
</script>

<style>
#app {
  display: flex;
  width: 100%;
  align-items: center;
  justify-content: center;
  flex-direction: column;
}

.img {
  width: 420px;
  height: 420px;
  padding-top: 100px;
}

.timer {
  color: #ffffff;
  font-size: 70px;
  margin-top: -210px;
}

.area-btn {
  margin-top: 155px;
  display: flex;
}

.button {
  -webkit-user-select: none;
  -moz-user-select: none;
  width: 150px;
  background-color: #ffffff;
  font-size: 20px;
  border: 0;
  border-radius: 5px;
  text-align: center;
  margin-left: 15px;
  margin-right: 15px;
  padding: 6px;
  cursor: pointer;
}

.button:hover {
  opacity: 0.8;
  transition: all 0.50;
}

ul {
  text-align: center;
  padding: 0px;
}

ul li  {
  margin-top: 4px;
  padding: 15px;
  background-color: rgb(70, 70, 70);
  list-style: none;
  color: #ffffff;
  font-size: 18px;
  border-radius: 6px;
}

.list button {
  cursor: pointer;
  border: 0;
  background-color: #ffffff;
  padding: 8px;
  border-radius: 5px;
  margin-bottom: 12px;
}
</style>
