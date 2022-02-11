<template>
  <div class="tabata-form">
      <div class="form name">
      <label for="name">Name</label>
      <my-input id="name" placeholder='Name'></my-input>
      </div>
      <div class="form prep">
        <label for="prep">Preparation</label>
        <my-input id="prep" type='number' placeholder='Preparation'></my-input>   
      </div>
        <div class="form work">
        <label for="work">Work</label>
        <my-input id="work" type='number' placeholder='Work'></my-input>   
        </div>
        <div class="form rest">
        <label for="rest">Rest</label>
        <my-input id="rest" type='number' placeholder='Rest'></my-input>   
        </div>
        <div class="form cycles">
        <label for="cycles">Cycles</label>
        <my-input id="cycles" type='number' placeholder='Cycles'></my-input>   
        </div>
        <div class="form color">
        <my-select :options='optionsColor'></my-select>  
        </div>
  </div>
</template>

<script>
export default {
    name: 'tabata-form',
    data(){
        return {
            colorFromForm: '',
            optionsColor: ['green', 'red', 'blue']
        }
    }
}
</script>

<style>
.form{ 
    margin-bottom: 1vh;
}
#name, 
#prep, 
#work, 
#rest, 
#cycles{
    margin: 0 auto;
    max-width: 50vw;
}
</style>