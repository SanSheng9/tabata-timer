<template>
  <div class="tabata-form">
      <div class="buttons new" v-if="viewButtons == 'new'">
        <div class="add">
            <img src="@/assets/cancel.svg" alt="" @click='createTabata'>
        </div>
        <div class="cancel" @click="$emit('edit')">
            <img src="@/assets/cancel.svg" alt="">
        </div>
        </div>
        <div class="buttons old" v-if="viewButtons == 'old'">
        <div class="set" @click="createTabata">
            <img src="@/assets/edit.svg" alt="">
        </div>     
      </div>
      <div class="form name">
      <label for="name">Name</label>
      <my-input id="name" v-model="tabataName" :style="{minWidth: 80 + '%'}" :value='tabataName' :maxlength='20'></my-input>
      </div>
      <div class="form prep">
        <label for="prep">Preparation</label>
        <div class="flex-box">
      <div class="plus" @click="tabataPrep++"><img src="@/assets/plus.svg" alt=""></div>
      <my-input id="prep" v-model='tabataPrep' :value='tabataPrep' :maxlength="2"></my-input>
      <div class="minus" @click="minusNumber('prep')" ><img src="@/assets/minus.svg" alt=""></div>      
      </div></div>
        <div class="form work">
        <label for="work">Work</label>
                <div class="flex-box">
        <div class="plus" @click="tabataWork++"><img src="@/assets/plus.svg" alt=""></div>
      <my-input id="work" v-model='tabataWork'   :value='tabataWork' :maxlength="2"></my-input>
      <div class="minus" @click="minusNumber('work')"><img src="@/assets/minus.svg" alt=""></div>      
      </div></div>
        <div class="form rest">
        <label for="rest">Rest</label>
    <div class="flex-box">
    <div class="plus" @click="tabataRest++"><img src="@/assets/plus.svg" alt=""></div>
      <my-input id="rest" v-model="tabataRest" :value='tabataRest' :maxlength="2"></my-input>
      <div class="minus" @click="minusNumber('rest')"><img src="@/assets/minus.svg" alt=""></div>      
       </div></div>
        <div class="form cycles">
        <label for="cycles">Cycles</label>
        <div class="flex-box">
        <div class="plus" @click="tabataCycles++"><img src="@/assets/plus.svg" alt=""></div>
      <my-input id="cycles" v-model="tabataCycles" :value='tabataCycles' :maxlength="1"></my-input>
      <div class="minus" @click="minusNumber('cycles')"><img src="@/assets/minus.svg" alt=""></div>      
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
        id: {
            type: Number,
            required: true
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
        },
        count: {
            type: Number,
            default: 2
        }
    },
    data(props){
        return {
            colorFromForm: '',
            tabataName: props.name,
            tabataId: props.id,
            tabataPrep: props.prep,
            tabataWork: props.work,
            tabataRest: props.rest,
            tabataCycles: props.cycles,
            tabataColor: props.color,
            newTabata: [],
            viewButtons: props.view,
            countId: props.count
        }
    },
    methods: {
        changeColor(color){
            this.tabataColor = color
            this.$emit('colorform', color)
        },
        createTabata(){
            if (this.viewButtons == 'new') {
                this.tabataId = this.countId
                this.countId = this.countId + 1
                this.$emit('count', this.countId)
            }
            this.newTabata = 
                {
                    name: this.tabataName,
                    id: this.tabataId,
                    color: this.tabataColor,
                    prep: this.tabataPrep,
                    work: this.tabataWork,
                    rest: this.tabataRest,
                    cycles: this.tabataCycles,
                },               
            this.$emit('create', this.newTabata)
            console.log('1:', this.newTabata)
            if (this.viewButtons == 'new') {this.$emit('colorform', 'grey')} 
            this.$emit('edit')           
        },
        minusNumber(number){
            if (number == 'prep') {
                if (this.tabataPrep != 0) {
                    this.tabataPrep--
                }
            }
            if (number == 'work') {
                if (this.tabataWork != 0) {
                    this.tabataWork--
                }
            }
            if (number == 'rest') {
                if (this.tabataRest != 0) {
                    this.tabataRest--
                }
            }
            if (number == 'cycles') {
                if (this.tabataCycles != 1) {
                    this.tabataCycles--
                }
            }
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
    overflow: hidden;
}
.form.name{
    display: flex;
    flex-direction: column;
}
.tabata-form .add,
.tabata-form .cancel,
.tabata-form .play,
.tabata-form .set{
    max-width: 12vw;
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