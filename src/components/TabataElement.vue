<template>
<div class="elements">
<my-element :tumbler='tumblerEdit' class="element">
    <div class="block">
        <div class="block-text">
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

            </div>
        </div>
        <div class="block-buttons">
                    <div class="play">
                        <img src="@/assets/play.svg" alt="">
                    </div>
                    <div class="edit" @click="openEdit">
                        <img src="@/assets/edit.svg" alt="">
                    </div>   
        </div>
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
            colorElemHover: 'dark' + String(props.tab.color),
            tumblerEdit: false
        }
    },
    methods: {
        secondsToHms(d) {
            d = Number(d);
            var h = Math.floor(d / 3600);
            var m = Math.floor(d % 3600 / 60);
            var s = Math.floor(d % 3600 % 60);
            return ('0' + h).slice(-2) + ":" + ('0' + m).slice(-2) + ":" + ('0' + s).slice(-2);
        },
        openEdit(){
            this.$emit('edit'),
            this.tumblerEdit = !this.tumblerEdit
        }
    }
}

</script>

<style scoped>
.element{
background-color: v-bind(colorElem);
}
.name{
    font-size: 28px;
    margin-bottom: 10px;
}

.element .play,
.element .edit{
    max-width: 11vw;
}
.element img{
    max-width: 100%;
}
.block{
    display: grid;
    grid-template-columns: 3fr 1fr;
}
.block-buttons{
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: space-evenly;
}
</style>