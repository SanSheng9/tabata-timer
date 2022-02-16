<template>
<div class="tabata-block">
<tabata-element v-for="tab in tabata" :key="tab.id" :tab="tab" @option='optionTabata'></tabata-element>
<my-element class="create" :tumbler='tumbleForm'>
        <p v-if="tumblerForm == false" @click="openEdit">Create new tabata? </p>
        <tabata-form @edit='openEdit' :view='view' :count='count' @count='changeCount' @colorform='changeColorTabataCreate' @create='openAndGoNewTabata' v-if="tumblerForm == true"></tabata-form>
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
            colorTabataCreate: 'gray',
            tabataId: '',
            view: 'new',
            count: 2,
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