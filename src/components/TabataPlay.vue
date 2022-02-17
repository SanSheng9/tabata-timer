<template>
  <div class="tabata-timer">
      <div class="timer">
        <div class="timer-line"></div>
        <div class="timer-body">
            <div class="timer-couner">
                <span class="second">1</span>
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
        }
    },
    data(){
        return {
        }
    },
    methods: {
        progressView(){
            let diagramBox = document.querySelectorAll('.diagram.progress');
            diagramBox.forEach((box) => {
            let deg = (360 * box.dataset.percent / 100) + 180;
            if(box.dataset.percent >= 50){
                box.classList.add('over_50');
             }else{
            box.classList.remove('over_50');
            }
            box.querySelector('.piece.right').style.transform = 'rotate('+deg+'deg)';
            });
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
      display: flex;
    justify-content: center;
    align-items: center;
}
.timer{
    width: 200px;
    height: 200px;
    border-radius: 50%;
    background-color: #fff;
    overflow: hidden;
    position: relative;
}

</style>