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
            currentTime: 0,
            duration: 0,
        }
    },
    methods: { 
        startTimer(cycl) {
                let count = cycl
                new Promise((resolve) => {
                    // Preparation
                let preparation = this.prep
                if (this.cycles == count) {
                console.log('Start Prep')
                this.currentTime = preparation
                this.timer = setInterval(() => {
                this.currentTime--
                if (this.currentTime <= 0)
                    {
                        resolve(console.log('Finish Prep'))
                        clearTimeout(this.timer)  
                    }
                }, 1000)} else {
                    resolve(console.log('No Prep'))
                }
                }).then(() => {
                    // Work
                    new Promise((resolve) => {
                        console.log('Start Work')
                        this.currentTime = this.work
                        this.timer = setInterval(() => {
                        this.currentTime--
                        if (this.currentTime <= 0)
                            {
                            resolve(console.log('Finish Work'))
                            clearTimeout(this.timer)  
                    }
                    }, 1000)
                    }).then(() => {
                        // Rest
                        new Promise((resolve) => {
                        console.log('Start Rest')
                        this.currentTime = this.rest
                        this.timer = setInterval(() => {
                        this.currentTime--
                        if (this.currentTime <= 0)
                            {
                            resolve(
                            console.log('Finish Rest'))
                            clearTimeout(this.timer)  
                    }
                    }, 1000)
                    }).then(() => {
                        new Promise((resolve) => {
                        console.log('Cycles - ', count)
                        if (count > 1) {
                            count--
                            resolve(
                            this.startTimer(count))
                        }
                        })
                    })
                    })
                    }
                    )
        },
    },
    watch: {
        animation: function () {
            this.startTimer(this.cycles)
        },
      //  currentTime(time) {
        //    if (time === 0) {
       //         this.stopTimer()
       //     }
       // }
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
    animation-name: mask_left;
    animation-duration: v-bind(currentTime);
    animation-timing-function: steps(1, end);
    animation-fill-mode: forwards;
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
    animation-name: mask_right;
    animation-duration: v-bind(currentTime);
    animation-timing-function: steps(1, end);
    animation-fill-mode: forwards;
    animation-play-state: v-bind(animation);

}
.timer-line {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    z-index: 2;
    animation-name: line;
    animation-duration: v-bind(currentTime);
    animation-timing-function: linear;
    animation-fill-mode: forwards;
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