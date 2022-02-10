<template>
<tabata-list :tabata='tabataArray'>

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
                    name: 'Light',
                    color: 'green',
                    prep: 10,
                    work: 20,
                    rest: 10,
                    cycles: 2,
                },
                {
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

    }
}
</script>

<style>

</style>