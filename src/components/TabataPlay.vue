<template>
  <div class="tabata-timer">
      <div class="timer">
        <div class="diagram progress" data-percent="18" @click='progressView'>
    <div class="piece left"></div>
    <div class="piece right"></div>
    <div class="text">
        <div>
            <b>18</b>
            <span>PERCENT</span>
        </div>
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
}
.timer{
}
.diagram {
    margin: 0 auto;
    width: 250px;
    height:250px;
    border-radius: 50%;
    background: #990;
    position: relative;
    overflow: hidden;
}
.diagram::before {
    content: '';
    display: block;
    position: absolute;
    top:20px;
    left:20px;
    right:20px;
    bottom:20px;
    border-radius: 50%;
    background: #ccc;
    z-index: 3;
    opacity: 1;
}
.diagram .piece {
    width: 100%;
    height: 100%;
    left: 0;
    right: 0;
    overflow: hidden;
    position: absolute;
}
.diagram .piece::before {
    content: '';
    display: block;
    position: absolute;
    width: 50%;
    height: 100%;
}
.diagram .piece.left {
    transform: rotate(0deg);
    z-index: 2;
    border-radius: 50%; /* only FireFox < 75.0v (fix bug)*/
}
.diagram.over_50 .piece.left {
    transform: rotate(180deg);
}
.diagram .piece.right {
    transform: rotate(180deg);
    z-index: 1;
    border-radius: 50%; /* only FireFox < 75.0v (fix bug)*/
}
.diagram.over_50 .piece.right {
    transform: rotate(360deg);
}
.diagram .left::before {
    background: #059;
}
.diagram.over_50 .left::before {
    background: #990;
}
.diagram .right::before {
    background: #059;
}
.diagram .text {
    position: absolute;
    z-index: 3;
    top: 0;
    bottom: 0;
    left:0;
    right:0;
    text-align: center;
    display: flex;
    align-items: center;
    justify-content: center;
}
.diagram .text b {
    font-size: 72px;
}
.diagram .text span {
    font-size: 16px;
    display: block;
}

</style>