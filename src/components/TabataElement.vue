<template>
<div class="elements">
<my-element :tumbler='tumblerEdit' class="element">
    <div class="block" >
        <div v-if="!tumblerEdit" class="block-text">
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
                    Time: {{secondsToHms(((tab.work + tab.rest) * tab.cycles) + tab.prep)}}
                </div>

            </div>
        </div>
        <div class="block-buttons" v-if='!tumblerEdit'>
                    <div class="play">
                        <img src="@/assets/play.svg" alt="">
                    </div>
                    <div class="edit" @click="openEdit">
                        <img src="@/assets/edit.svg" alt="">
                    </div>   
        </div>
        <tabata-form v-if="tumblerEdit" 
        :name='tab.name'
        :id='tab.id' 
        :prep='tab.prep' 
        :work='tab.work'
        :rest='tab.rest'
        :cycles='tab.cycles'
        :view='view'
        :color='tab.color'
        @edit='openEdit'
        @create='optionTabata'
        @colorform='changeColorElement'
        class="block-edit"></tabata-form>
    </div>
</my-element>
</div>
</template>

<script>
import TabataForm from "@/components/TabataForm.vue"

export default {
    components: {
        TabataForm
    },
    name: 'tabata-element',
    props: {
        tab: {
            type: Object,
            required: true
        }
    },
    data(props){
        return{
            colorElem: String(props.tab.color),
            colorElemHover: 'dark' + String(props.tab.color),
            tumblerEdit: false,
            view: 'old',
            viewblock: 'row',
            viewbuttons: 'column'
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
            var arr = [this.viewblock, this.viewbuttons]
            arr.reverse
            this.viewbuttons= arr[0]
            this.viewblock = arr[1]
        },
        optionTabata(element){
            this.$emit("option", element)
            console.log('2:', element)
        },
        changeColorElement(color){
            this.colorElem = String(color)
        }
    },
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
    max-width: 12vw;
}
.element img{
    max-width: 100%;
}
.block{
    display: flex;
    justify-content: space-between;
    flex-direction: v-bind(viewblock);
}
.block-buttons{
    display: flex;
    align-items: center;
    justify-content: space-around;
    margin-right: 3vw;
    transition: flex 0.2s linear 0s;
    flex-direction: v-bind(viewbuttons);    
}

</style>