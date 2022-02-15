<template>
<div class="elements">
<my-element :tumbler='tumblerEdit' class="element">
    <div class="block" >
        <div v-if="!tumblerEdit" class="block-text">
            <div class="name">
                {{name}}
            </div>
            <div class="options">
                <div class="prep">
                    Preparation: {{prep}} sec
                </div>
                <div class="work">
                    Work: {{work}} sec
                </div>
                <div class="rest">
                    Rest: {{rest}} sec
                </div>
                <div class="cycles">
                    Cycles: {{cycles}} sec
                </div>
                <div class="time">
                    Time: {{secondsToHms(((this.work + this.rest) * this.cycles) + this.prep)}}
                </div>

            </div>
        </div>
        <div class="block-buttons" :class='{option: tumblerEdit}'>
                    <div class="play">
                        <img src="@/assets/play.svg" alt="">
                    </div>
                    <div class="edit" @click="openEdit" >
                        <img src="@/assets/edit.svg" alt="">
                    </div>   
        </div>
        <tabata-form v-if="tumblerEdit" 
        :name='name' 
        :prep='prep' 
        :work='work'
        :rest='rest'
        :cycles='cycles'
        :view='view'
        :color='color'
        @create='openAndGoNewTabata'
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
    data({ tab }){
        return{
            name: tab.name,
            work: tab.work,
            prep: tab.prep,
            rest: tab.rest,
            cycles: tab.cycles,
            color: tab.color,
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
        openAndGoNewTabata(tabata){
            this.$emit('change', tabata)
        }
    }
}

</script>

<style scoped>
.element{
background-color: v-bind(color);
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
    flex-direction: v-bind(viewbuttons);    
}
.block-buttons.option{
    flex-direction: row;
    flex: 1 1 auto;
    margin-right: 0;
    margin-top: 3vw;
}

.block-buttons.option .play{
}
</style>