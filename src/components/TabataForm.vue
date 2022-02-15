<template>
  <div class="tabata-form">
      <div class="buttons" v-if="viewButtons == 'new'">
        <div class="add">
            <img src="@/assets/cancel.svg" alt="" @click='createTabata'>
        </div>
        <div class="cancel" @click="$emit('edit')">
            <img src="@/assets/cancel.svg" alt="">
        </div>   
      </div>
      <div class="form name">
      <label for="name">Name</label>
      <my-input id="name" v-model="tabataName" :style="{minWidth: 80 + '%'}" :value='tabataName'></my-input>
      </div>
      <div class="form prep">
        <label for="prep">Preparation</label>
        <div class="flex-box">
      <div class="plus" @click="tabataPrep++"><img src="@/assets/plus.svg" alt=""></div>
      <my-input id="prep" v-model='tabataPrep' :value='tabataPrep'></my-input>
      <div class="minus" @click="tabataPrep--" ><img src="@/assets/minus.svg" alt=""></div>      
      </div></div>
        <div class="form work">
        <label for="work">Work</label>
                <div class="flex-box">
        <div class="plus" @click="tabataWork++"><img src="@/assets/plus.svg" alt=""></div>
      <my-input id="work" v-model='tabataWork'   :value='tabataWork'></my-input>
      <div class="minus" @click="tabataWork--"><img src="@/assets/minus.svg" alt=""></div>      
      </div></div>
        <div class="form rest">
        <label for="rest">Rest</label>
    <div class="flex-box">
    <div class="plus" @click="tabataRest++"><img src="@/assets/plus.svg" alt=""></div>
      <my-input id="rest" v-model="tabataRest" :value='tabataRest'></my-input>
      <div class="minus" @click="tabataRest--"><img src="@/assets/minus.svg" alt=""></div>      
       </div></div>
        <div class="form cycles">
        <label for="cycles">Cycles</label>
        <div class="flex-box">
        <div class="plus" @click="tabataCycles++"><img src="@/assets/plus.svg" alt=""></div>
      <my-input id="cycles" v-model="tabataCycles" :value='tabataCycles'></my-input>
      <div class="minus" @click="tabataCycles--"><img src="@/assets/minus.svg" alt=""></div>      
      </div></div>
        <div class="form color">
            <div class="color" :style="{paddingBottom: 10 + 'px'}">Color</div>
            <div class="conteiner">
                <div class="col pink" @click='changeColor("pink")'>PINK</div>
                <div class="col blue" @click='changeColor("blue")'>BLUE</div>
                <div class="col cyan" @click='changeColor("cyan")'>CYAN</div>
                <div class="col red" @click='changeColor("red")'>RED</div>
                <div class="col green" @click='changeColor("green")'>GREEN</div>
                <div class="col purple" @click='changeColor("purple")'>PURPLE</div>
            </div>
        </div>
  </div>
</template>

<script>
export default {
    name: 'tabata-form',
    props: {
        name: {
            type: String,
            default: 'My Tabata'
        },
        color: {
            type: String,
            default: 'gray'
        },
        prep: {
            type: Number,
            default: 10
        },
        work: {
            type: Number,
            default: 20
        },
        rest: {
            type: Number,
            default: 10
        },
        cycles: {
            type: Number,
            default: 3
        },
        view: {
            type: String,
            required: true
        }
    },
    data(props){
        return {
            colorFromForm: '',
            tabataName: props.name,
            tabataPrep: props.prep,
            tabataWork: props.work,
            tabataRest: props.rest,
            tabataCycles: props.cycles,
            tabataColor: 'gray',
            newTabata: [],
            viewButtons: props.view
        }
    },
    methods: {
        changeColor(color){
            this.tabataColor = color
            this.$emit('colorform', color)
        },
        createTabata(){
            this.newTabata = 
                {
                    name: this.tabataName,
                    color: this.tabataColor,
                    prep: this.tabataPrep,
                    work: this.tabataWork,
                    rest: this.tabataRest,
                    cycles: this.tabataCycles,
                },               
            this.$emit('create', this.newTabata)
            this.$emit('colorform', 'grey') 
            this.$emit('edit')           
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
    margin-bottom: 15px;
}
.buttons{
    display: flex;
    align-items: center;
    justify-content: space-evenly;
    margin-bottom: 2vh;
}
.form.name{
    display: flex;
    flex-direction: column;
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
    max-width: 10vw
}
.flex-box{
    display: flex;
    align-items: center;
    justify-content: space-evenly;
}
.conteiner{
    background-color: white;
    max-width: 80%;
    margin: 0 auto;
    padding: 10px;
        font-size: 36px;

}
.pink {
    background-color: pink;
}
.blue {
    background-color: blue;
}
.cyan {
    background-color: cyan;
    color: gray;
}
.red {
    background-color: red;
}
.green {
    background-color: green;
}
.purple {
    background-color: purple;
}
.col{
}
</style>