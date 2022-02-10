<template>
<div class="tabata-block">
<tabata-element v-for="tab in tabata" :key="tab.id" :tab="tab"></tabata-element>
<div class="element create">
    <div class="container">
        Create new tabata?
    </div>
</div>
</div>
</template>

<script>
import TabataElement from "@/components/TabataElement.vue"

export default {
    name: 'tabata-list',
    components: {
        TabataElement
    },
    props: {
        tabata: {
            type: Array,
            required: true
        }
    }
}
</script>

<style>
.tabata-block{
    padding-left: 1vw;
    padding-right: 1vw;
    padding-top: 1vw;
    padding-bottom: 1vw;
}
.element.create{
    background-color: gray;
    text-align: center;
    font-size: 32px;
    
}
</style>