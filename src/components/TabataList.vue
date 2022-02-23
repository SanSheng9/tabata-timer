<template>
<div class="tabata-block">
<tabata-play v-show="showPlay" class="tabata-play" 
:color='colorElementPlayed'
 :work='workPlay' 
 :prep='prepPlay'
 :rest='restPlay'
 :cycles='cyclesPlay'
 :animation='animationPlayedState'
 :play='playTumbler'
 @finish='finishTabata'
>
</tabata-play>
<div class="tabata-list">
<transition-group name="list">
<tabata-element v-for="tab in tabata" :key="tab.id" :tab="tab" @option='optionTabata' @play="playTabata"></tabata-element>
</transition-group>
<my-element class="create" :tumbler='tumbleForm'>
        <p v-if="tumblerForm == false" @click="openEdit">Create new tabata? </p>
        <tabata-form @edit='openEdit' :view='view' :count='count' @count='changeCount' @colorform='changeColorTabataCreate' @create='openAndGoNewTabata' v-if="tumblerForm == true"></tabata-form>
</my-element>
</div>
</div>
</template>

<script>
import TabataElement from "@/components/TabataElement.vue"
import TabataForm from "@/components/TabataForm.vue"
import TabataPlay from "@/components/TabataPlay.vue"

export default {
    name: 'tabata-list',
    components: {
        TabataElement,
        TabataForm,
        TabataPlay
    },
    props: {
        tabata: {
            type: Array,
            required: true
        }
    },
    data(){
        return{
            tumblerForm: false,
            colorTabataCreate: 'gray',
            tabataId: '',
            view: 'new',
            count: 2,
            colorElementPlayed: '',
            elemPlayed: '',
            topPlay: -101 + '%',
            leftPlay: -1 + '%',
            position: 'block',
            animationPlayedState: 'paused',
            workPlay: '',
            prepPlay: '',
            restPlay: '',
            cyclesPlay: '',
            playTumbler: false,
            showPlay: false
            }
    },
    methods: {
        changeColorTabataCreate(color){
            this.colorTabataCreate = color
        },
        
        openEdit(){
            this.tumblerForm = !this.tumblerForm
        },
        openAndGoNewTabata(newTabata){
            this.$emit("create", newTabata)
            this.newTabataFromForm = newTabata
        },
        optionTabata(element){
            console.log('3,2:', element)
            this.$emit('option', element)
        },
        changeCount(countId){
            this.count = countId
        },
        playTabata(elem){
            this.workPlay = elem.work
            this.prepPlay = elem.prep
            this.restPlay = elem.rest
            this.cyclesPlay = elem.cycles
            this.colorElementPlayed = elem.color
            this.position = 'fixed'
            this.playTumbler = !this.playTumbler
            this.showPlay = true
            this.animationPlayedState = 'running'
        },
        finishTabata(){
            this.position = 'static'
            this.showPlay = false
            this.animationPlayedState = 'paused'
        }
    }
}
</script>

<style>
.tabata-block{
    padding-left: 1vh;
    padding-right: 1vh;
    padding-top: 1vh;
    padding-bottom: 1vh;
    position: v-bind(position);
    width: 100%;
}
.element.create{
    background-color: v-bind(colorTabataCreate);
    text-align: center;
    font-size: 32px;
    
}
.list-element {
  display: inline-block;
  margin-right: 10px;
}
.list-enter-active,
.list-leave-active {
  transition: all 1s ease;
}
.list-enter-from,
.list-leave-to {
  opacity: 0;
  transform: translateY(30px);
}
.tabata-list{
}
.tabata-play{
    min-height: 103vh;
    min-width: 103vw;
    position: fixed;
    top: 0;
    left: 0;
}
</style>