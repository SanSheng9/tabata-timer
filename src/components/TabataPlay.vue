<template>
  <div class="tabata-timer">
      <div class="all-time">
          <p>{{secondsToHms(globalCurrentTime)}}</p>
      </div>
      <div class="timer" :class='{animation: animClass}'>
        <div class="timer-line" :class='{animation: animClass}'></div>
        <div class="timer-body">
            <div class="timer-couner">
                <span class="second">{{ currentTime }}
                </span>
            </div>
        </div>
      </div>
      <div class="stage">
          <p>{{stage}}</p>
      </div>
      <div class="next-stage">
          <p>{{nextStage}}</p>
      </div>
  </div>
</template>

<script>
export default {
    emit: 'finish',
    name: 'tabata-play',
    props: [
        'animation', 'color', 'work', 'rest', 'prep', 'cycles', 'play'
    ],
    data(){
        return {
            playStart: true,
            currentTime: 0,
            duration: 0,
            animClass: true,
            stage: '',
            globalTimer: 0,
            globalCurrentTime: 0, 
            nextStage: ''
        }
    },
    methods: {
        addDeleteClass() {
                this.animClass = false
                console.log('animation')
                setTimeout(() => {this.animClass = true}, 20)
        },
        finishTabata(){
            this.$emit('finish')
        },
        startTimer(cycl) {
                let count = cycl
                new Promise((resolve) => {
                    // Preparation
                let preparation = this.prep
                if (this.cycles == count && preparation > 0) {
                console.log('Start Prep')
                this.currentTime = preparation
                //
                this.addDeleteClass()  
                //            
                this.duration = this.currentTime + 's'
                this.stage = 'Preparation'
                this.nextStage = 'Work'
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
                        this.currentTime = 0
                        this.currentTime = this.work
                //
                this.addDeleteClass()  

                //                                    
                        this.duration = this.currentTime + 's'
                        this.stage = 'Work'
                        this. nextStage = 'Rest'
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
                        this.currentTime = 0
                        this.currentTime = this.rest
                //
                this.addDeleteClass()  
                //                                    
                        this.duration = this.currentTime + 's'
                        this.stage = 'Rest'
                        if (count <= 1 ) {this.nextStage = 'Finish'} else {this.nextStage = 'Work'}
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
                        } else if (count <= 1) {console.log('ELSE')
                        this.finishTabata()
                        }
                        })
                    })
                    })
                    }
                    )
        },
        startGlobalTimer(){
                this.globalCurrentTime = ((this.work + this.rest) * this.cycles) + this.prep
                this.globalTimer = setInterval(
                    () => {
                        this.globalCurrentTime--
                        if ( this.globalCurrentTime <= 0) {clearTimeout(this.globalTimer)}
                    }, 1000
                )
        },
         secondsToHms(d) {
            d = Number(d);
            var h = Math.floor(d / 3600);
            var m = Math.floor(d % 3600 / 60);
            var s = Math.floor(d % 3600 % 60);
            return ('0' + h).slice(-2) + ":" + ('0' + m).slice(-2) + ":" + ('0' + s).slice(-2);
        },
    },
    watch: {
        play: function () {
            this.startTimer(this.cycles)
            this.startGlobalTimer()
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
.timer.animation::before {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    width: 50%;
    height: 100%;
    z-index: 3;
    background-color: #333;
    animation-name: mask_left;
    animation-duration: v-bind(duration);
    animation-timing-function: steps(1, end);
    animation-fill-mode: backwards;
    animation-play-state: v-bind(animation);

}
.timer.animation::after {
    content: '';
    position: absolute;
    top: 0;
    right: 0;
    width: 50%;
    height: 100%;
    z-index: 3;
    background-color: white;
    animation-name: mask_right;
    animation-duration: v-bind(duration);
    animation-timing-function: steps(1, end);
    animation-fill-mode: backwards;
    animation-play-state: v-bind(animation);

}
.timer-line.animation {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    z-index: 2;
    animation-name: line;
    animation-duration: v-bind(duration);
    animation-timing-function: linear;
    animation-fill-mode: backwards;
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
.stage {   
    transition: all 1s ease 0s;
}
.stage p{
    font-size: 40px;
    color: white;
    text-align: center;
    margin-top: 6vh;
    text-transform: uppercase;
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