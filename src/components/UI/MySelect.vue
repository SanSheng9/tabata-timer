<template>
  <select :value="modelValue" @change="changeOptions" class="select">
      <option disabled value="">Select from the list...</option>
      <option 
      v-for='option in options' 
      :key="option.value" 
      :value="option.value">
      {{option.name}}</option>
  </select>
</template>

<script>
export default {
    emit: ['update:modelValue'],
    name: 'my-select',
    props: {
        modelValue: {
            type: String
        },
        options: {
            type: Array,
            default: () => []
        }
    },
    methods: {
        changeOptions(event) {
            this.$emit('update:modelValue', event.target.value)
        }
    }
}
</script>

<style scoped>
.select{
   border: 2px solid white;
   height: 2em;
   background-color: rgba(0, 0, 0, 0);
   width: 100%;
   color: rgb(255, 255, 255);
   outline: none;
}
.select:focus{
    border: 2px solid darkgray;
}
</style>