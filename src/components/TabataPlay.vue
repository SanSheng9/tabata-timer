<template>
  <div class="tabata-timer">
      <div class="timer">
        <div class="timer-line"></div>
        <div class="timer-body">
            <div class="timer-couner">
                <span class="second">{{ currentTime }}
                </span>
            </div>
        </div>
      </div>
  </div>
</template>

<script>
export default {
    name: 'tabata-play',
    props: [
        'animation', 'color', 'work', 'rest', 'prep', 'cycles'
    ],
    data(){
        return {
            workPlayed: this.work,
            prepPlayed: this.prep,
            restPlayed: this.rest,
            cyclesPlayed: this.cycles,
            time: ((this.work + this.rest) * this.cycles) + this.prep,
            currentTime: 0
        }
    },
    methods: { 
        startTimer() {
            this.currentTime = this.time
            setTimeout(() => {
             this.timer = setInterval(() => {
            this.currentTime--}, 1000)   
            }, 1000);
            
        },
        stopTimer() {
            clearTimeout(this.timer)
        },
    },
    watch: {
        animation: function () {
            this.startTimer()
        },
        currentTime(time) {
            if (time === 0) {
                this.stopTimer()
            }
        }
    },
    
}
</script>

<style>
.tabata-timer{
  background-color: v-bind(color);
  transition: background-color 0.5s ease 0s;
  min-height: 100vh;
  min-width: 100vw;
  z-index: 1;
  animation-play-state: v-bind(animation);  
}
.timer{
    width: 55vw;
    height: 55vw;
    border-radius: 50%;
    background-color: #333;
    overflow: hidden;
    margin: 0 auto;
    margin-top: 200px;
    position: relative;
    display: flex;
    justify-content: center;
    align-items: center;
    z-index: 2;
}
.timer::before {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    width: 50%;
    height: 100%;
    z-index: 3;
    background-color: #333;
    animation: mask_left 1s steps(1, end) forwards;
    animation-duration: v-bind(currentTime);
      animation-play-state: v-bind(animation);  

}
.timer::after {
    content: '';
    position: absolute;
    top: 0;
    right: 0;
    width: 50%;
    height: 100%;
    z-index: 3;
    background-color: white;
    animation: mask_righ 1s steps(1, end) forwards;
        animation-duration: v-bind(currentTime);

      animation-play-state: v-bind(animation);  

}
.timer-line {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    z-index: 2;
    animation: line 10s linear forwards;
        animation-duration: v-bind(currentTime);

      animation-play-state: v-bind(animation);  

}
.timer-line::after{
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    width: 50%;
    height: 100%;
    background-color: white;
}
.timer-body{
    width: 80%;
    height: 80%;
    border-radius: 50%;
    background-color: v-bind(color);
    overflow: hidden;
    display: flex;
    justify-content: center;
    align-items: center;
    z-index: 4;
}
.timer-counter{
}
.second{
    font-size: 48px;
    color: white;
}

@keyframes line {
    0% {

    }
    100% {
        transform: rotate(360deg)
    }
}

@keyframes mask_left {
    0% {
        visibility: visible;
    }
    50%, 100%{
        visibility: hidden;
    }
    
}
@keyframes mask_right {
    0% {
        visibility: hidden;
    }
    50%, 100%{
        visibility: visible;
    }
    
}
</style>