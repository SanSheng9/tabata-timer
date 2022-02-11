<template>
  <input :value='modelValue' @input="updateInput" class="input" type="text">
</template>

<script>
export default {
   name: 'my-input',
   props: {
      modelValue: [String, Number]
   },
   methods: {
      updateInput(event) {
         this.$emit('update:modelValue', event.target.value)
      }
   }
}
</script>

<style scoped>
.input {
   border: 2px solid white;
   height: 2em;
   background-color: rgba(0, 0, 0, 0);
   width: 100%;
   color: rgb(255, 255, 255);
   outline: none;
   transition: all 1s ease 0s;
   
}
.input:focus{
   font-size: 24px;
}
input::placeholder{
   color: rgb(218, 218, 218)
}
</style>