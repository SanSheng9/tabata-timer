<template>
  <div class="tabata-form">
      <div class="buttons">
        <div class="add">
            <img src="@/assets/cancel.svg" alt="">
        </div>
        <div class="cancel" @click="$emit('edit')">
            <img src="@/assets/cancel.svg" alt="">
        </div>   
      </div>
      <div class="form name">
      <label for="name">Name</label>
      <my-input id="name" placeholder='Name'></my-input>
      </div>
      <div class="form prep">
        <label for="prep">Preparation</label>
        <div class="flex-box">
      <div class="plus"><img src="@/assets/plus.svg" alt=""></div>
      <my-input id="prep" placeholder='prep'></my-input>
      <div class="minus"><img src="@/assets/minus.svg" alt=""></div>      
      </div></div>
        <div class="form work">
        <label for="work">Work</label>
                <div class="flex-box">
        <div class="plus"><img src="@/assets/plus.svg" alt=""></div>
      <my-input id="work" placeholder='Work'></my-input>
      <div class="minus"><img src="@/assets/minus.svg" alt=""></div>      
      </div></div>
        <div class="form rest">
        <label for="rest">Rest</label>
    <div class="flex-box">
    <div class="plus"><img src="@/assets/plus.svg" alt=""></div>
      <my-input id="rest" placeholder='Rest'></my-input>
      <div class="minus"><img src="@/assets/minus.svg" alt=""></div>      
       </div></div>
        <div class="form cycles">
        <label for="cycles">Cycles</label>
        <div class="flex-box"><div class="plus"><img src="@/assets/plus.svg" alt=""></div>
      <my-input id="cycles" placeholder='Cycles'></my-input>
      <div class="minus"><img src="@/assets/minus.svg" alt=""></div>      
      </div></div>
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
.buttons{
    display: flex;
    align-items: center;
    justify-content: space-evenly;
    margin-bottom: 2vh;
}
.tabata-form .add,
.tabata-form .cancel{
    max-width: 11vw;
}
.tabata-form .add{
    transform: rotate(45deg);
}
.tabata-form img{
    max-width: 100%;
    margin: auto 0;
}
.form .plus,
.form .minus{
    max-width: 8vw
}
.flex-box{
    display: flex;
    align-items: center;
    justify-content: space-evenly;
}
</style>