<template>
<div class="elements">
  <div class="element">
    <div class="container">
        <div class="block-1">
            <div class="name">
                {{tab.name}}
            </div>
            <div class="options">
                <div class="prep">
                    Preparation: {{tab.prep}} sec
                </div>
                <div class="work">
                    Work: {{tab.work}} sec
                </div>
                <div class="rest">
                    Rest: {{tab.rest}} sec
                </div>
                <div class="cycles">
                    Cycles: {{tab.cycles}} sec
                </div>
                <div class="time">
                    Time: {{secondsToHms(time)}}
                </div>
                <div class="buttons"></div>
            </div>
        </div>
        <div class="block-2">
        </div>   
    </div>
  </div>
</div>
</template>

<script>
export default {
    name: 'tabata-element',
    props: {
        tab: {
            type: Object,
            required: true
        }
    },
    data(props){
        return{
            time: ((props.tab.work + props.tab.rest) * props.tab.cycles) + props.tab.prep,
            colorElem: String(props.tab.color),
            colorElemHover: 'dark' + String(props.tab.color)
        }
    },
    methods: {
        secondsToHms(d) {
            d = Number(d);
            var h = Math.floor(d / 3600);
            var m = Math.floor(d % 3600 / 60);
            var s = Math.floor(d % 3600 % 60);
            return ('0' + h).slice(-2) + ":" + ('0' + m).slice(-2) + ":" + ('0' + s).slice(-2);
        }
    }
}

</script>

<style>
.element{
max-width: 100%;
margin-bottom: 1vw;
color:azure;
font-size: 24px;
min-height: 55vw;
background-color: v-bind(colorElem);
}
.element:hover{
    background-color: v-bind(colorElemHover);
}
.container {
    max-width: 95%;
    margin: 0 auto;
    padding-top: 5%;
    padding-bottom: 5%;
}
.name{
    font-size: 28px;
    margin-bottom: 10px;
}
</style>