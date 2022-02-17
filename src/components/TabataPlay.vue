<template>
  <div class="tabata-timer">
      <div class="timer">
        <div class="timer-line"></div>
        <div class="timer-body">
            <div class="timer-couner">
                <span class="second">{{sec()}}
                </span>
            </div>
        </div>
      </div>
  </div>
</template>

<script>
export default {
    name: 'tabata-play',
    props: {
        color: {
            type: String,
            required: true
        },
        element: {
            type: Object,
            required: true
        },
        animation: {
            type: String,
            default: 'paused'
        }
    },
    data({element}){
        return {
            activatedElement: element,
            fullTime: ''
        }
    },
    methods: { 
        sec(){
            this.fullTime = ((this.activatedElement.work + this.activatedElement.rest) * this.activatedElement.cycles) + this.activatedElement.prep
            return setInterval(() => {
                if (this.work > 0) {
                    this.work - 1
                }
                return this.work
            }, this.fullTime);
            
        }

    }
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
    animation: mask_left 10s steps(1, end) forwards;
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
    animation: mask_right 10s steps(1, end) forwards;
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