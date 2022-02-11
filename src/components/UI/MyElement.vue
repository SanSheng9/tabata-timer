<template>
<div class="element" @click="openCloseElement" :class="{opened: tumblerElement}">
    <div class="container">
        <div class="content" @click.stop>
            <slot></slot>
        </div>
    </div>
</div>
</template>

<script>
export default {
    name: 'my-element',
    data() {
    return {
        tumblerElement: false
    }
    },
    methods: {
        openCloseElement(){
            this.tumblerElement = !this.tumblerElement
            this.$emit('tumbler', this.tumblerElement)
        }
    }
}
</script>

<style>
.element{
max-width: 100%;
margin-bottom: 1vw;
color:azure;
font-size: 24px;
min-height: 55vw;
background-color: v-bind(colorElem);
transition: all 1s ease 0s;
}
.container {
    max-width: 95%;
    min-height: 95%;
    margin: 0 auto;
    padding-top: 5%;
    padding-bottom: 5%;
}
.element.opened{
    position: absolute;
    top: 1vh;
    left: 1vh;
    z-index: 2;
    min-height: 98vh;
    min-width: 96vw;
}
.element.opened .content{

}
</style>