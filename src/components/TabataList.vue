<template>
<div class="tabata-block">
<tabata-element v-for="tab in tabata" :key="tab.id" :tab="tab"></tabata-element>
<my-element @tumbler='openOrCloseForm' class="create">
        <p v-if="tumblerForm == false">Create new tabata? </p>
        <tabata-form @color='changeColorTabataCreate' v-if="tumblerForm == true"></tabata-form>
</my-element>
</div>
</template>

<script>
import TabataElement from "@/components/TabataElement.vue"
import TabataForm from "@/components/TabataForm.vue"

export default {
    name: 'tabata-list',
    components: {
        TabataElement,
        TabataForm
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
            colorTabataCreate: 'gray'
        }
    },
    methods: {
        openOrCloseForm(tmblr){
            console.log(tmblr)
            this.tumblerForm = tmblr
        },
        changeColorTabataCreate(color){
            this.colorTabataCreate = color
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
}
.element.create{
    background-color: v-bind(colorTabataCreate);
    text-align: center;
    font-size: 32px;
    
}
</style>