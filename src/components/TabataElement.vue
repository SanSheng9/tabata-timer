<template>
<div class="elements">
<my-element class="element">
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
</my-element>
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

<style scoped>
.element{
background-color: v-bind(colorElem);
}
.element:hover{
background-color: v-bind(colorElemHover);
}
.name{
    font-size: 28px;
    margin-bottom: 10px;
}
</style>