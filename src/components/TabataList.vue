<template>
<div class="tabata-block">
<tabata-element v-for="tab in tabata" 
:key="tab.id" 
:tab="tab" 
@change='emit("change", tabata, tab.id)'>
</tabata-element>
<my-element class="create" :tumbler='tumbleForm'>
        <p v-if="tumblerForm == false" @click="openEdit">Create new tabata? </p>
        <tabata-form @edit='openEdit'
        @colorform='changeColorTabataCreate'
        :view='view' 
        @create='openAndGoNewTabata' 
        v-if="tumblerForm == true"></tabata-form>
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
            newTabataFromForm: '',
            view: 'new',
            colorTabataCreate: 'gray',
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