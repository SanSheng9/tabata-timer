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
   border: none;
   border-bottom: 2px solid white;
   height: 2em;
   background-color: rgba(0, 0, 0, 0);
   width: 100%;
   color: rgb(255, 255, 255);
   outline: none;
   text-align: center;
   transition: all 1s ease 0s;
   font-size: 28px;
}
.input:focus{
}
input::placeholder{
   color: rgb(218, 218, 218)
}
</style>