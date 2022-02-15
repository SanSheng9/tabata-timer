<template>
<tabata-list :tabata='tabataArray' @create='addTabata' @change='editTabata'>

</tabata-list>
</template>

<script>
import TabataList from "@/components/TabataList.vue"

export default {
    name: 'tabata',
    components: {
        TabataList
    },
    data() {
        return {
            tabataArray: [
                {
                    id: 0,
                    name: 'Light',
                    color: 'green',
                    prep: 10,
                    work: 20,
                    rest: 10,
                    cycles: 2,
                },
                {
                    id: 1,
                    name: 'Hard',
                    color: 'red',
                    prep: 10,
                    work: 30,
                    rest: 10,
                    cycles: 3
                }                
            ]
        }
    }, 
    methods: {
        addTabata(tabata){
            this.tabataArray.push(tabata)
        },
        editTabata(tabata, id){
            this.tabataArray.forEach((tab) =>{
                if (tab.id == id) {
                    tab = tabata
                }
            })
        }
    }
}
</script>

<style>

</style>