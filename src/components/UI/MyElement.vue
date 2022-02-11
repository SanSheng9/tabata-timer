<template>
<div class="element" :class="{opened: tumbler}">
    <div class="container">
        <div class="content">
            <slot></slot>
        </div>
    </div>
</div>
</template>

<script>
export default {
    name: 'my-element',
    props: {
        tumbler: {
            type: Boolean,
            default: false
        }
    },
    data() {
    return {
    }
    },
    methods: {

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
    position: relative;
    top: 0vh;
    left: 0vh;
    z-index: 2;
    min-height: 98vh;
    min-width: 96vw;
}
.element.opened .content{

}
</style>