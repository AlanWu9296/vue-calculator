<template >
    <div>
        <p @click="isShowHelp=!isShowHelp" style="color:grey;font-size:16px;margin-top:0px">show help</p>
        <div id="container" is="transition-group" name="show" appear>
                <div id="calculator" :key="1">
                    <transition name="slide" appear>
                        <display-bar :displayData="displayData" id="display" v-if="animStep>=1"/>
                    </transition>
                    <div id="func-pad" is="transition-group" name="slide" appear v-if="animStep>=2">
                        <sym-button v-for="item in symbols.slice(0,3)" :key="item" :name="item" :timeInterval="150" :keyCodeDict="codeDict" :eventName="'symClicked'" @symClicked="handleSymbol($event)"/>
                    </div>
                    <div id="num-pad" is="transition-group" name="pop" appear v-if="animStep>=3">
                        <num-button v-for="num in numbers" :key="num" :name="num" :timeInterval="150" :keyCodeDict="codeDict" :eventName="'numClicked'" @numClicked="changeDisplay($event)"/>
                    </div>
                    <div id="symbol-pad" is="transition-group" name="drop" appear >
                        <sym-button v-for="item in functions" :key="item" :name="item" :timeInterval="150" :keyCodeDict="codeDict" :eventName="'symClicked'" @symClicked="handleSymbol($event)"/>
                    </div>
                </div>
    
    
                <help-display v-if="isShowHelp" :key="2"/>
    
        </div>
    </div>
</template>

<script>
const _ = require('lodash')
import DisplayBar from "./DisplayBar"
import NumButton from "./NumButton"
import SymButton from "./SymButton"
import HelpDisplay from "./HelpDisplay"

let numbers = ['1','2','3','4','5','6','7','8','9','0',".","C"]
let symbols = ["AC","+/-","%",'+','-','*','/','=']
let codeDict = {
    '+':[107,187],
    '*':[108],
    '-':[109,189],
    '.':[110,190],
    '/':[111,191],
    '=':[108,13,32],
    'C':[8,46],
    'AC':[27],
    '+/-':[9]
}
let symbolDict = {
    '+':_.add,
    '-':_.subtract,
    '*':_.multiply,
    '/':_.divide,
    '=':a => a
}

export default {
    name:"calculator",
    data(){
        return {
            numbers,
            symbols:symbols.slice(0,3),
            functions:[],
            symbolDict,
            codeDict,
            displayData:"",
            isNew:true,
            isPrime:true,
            isShowHelp:false,
            memData: null,
            operator: null,
            animStep:null
        }
    },
    components:{
        DisplayBar,
        SymButton,
        NumButton,
        HelpDisplay,
    },
    mounted(){
        let self = this
        let i = 0
        let j = 0
        let id2 = setInterval(
            function(){
                if(j<=4){
                    self.animStep = j
                    j++
                }else{
                    clearInterval(id2)
                }
            },
            400
        )
        let functions = symbols.slice(3,10)
        let id = setInterval(
            function(){
                if(i<functions.length){
                    self.functions.push(functions[i])
                    i++
                }else{
                    setTimeout(function(){self.isShowHelp=true},2000)
                    setTimeout(function(){self.isShowHelp=false},10000)
                    clearInterval(id)
                }
            },
            200
        )
    },
    methods:{
        initialize(){
            this.isNew = true
            this.isPrime = true
            this.displayData = ""
            this.memData = null
            this.operator = null
        },

        calculate(operator,data){
            this.memData = this.symbolDict[operator](this.memData, data)
            this.displayData = this.memData.toString()
        },

        decide(operator,data){
            if(this.isNew){
                this.calculate(operator,data)
            }else{
                this.displayData = this.symbolDict[operator](parseInt(this.displayData), data).toString()
            }
            this.operator = null
        },

        changeDisplay(e){
            if (e!=="C"){
                if(this.isNew){
                    this.displayData = e
                    this.isNew = false
                }else{
                    this.displayData += e
                }
            } else{
                if(this.isNew){
                    this.initialize()
                }else{
                    let l = this.displayData.length
                    this.displayData = this.displayData.substr(0,l-1)
                }
            }
        },

        handleSymbol(e){
            if(e==="AC"){
                this.initialize()
            }
            else if(e==="+/-"){
                this.decide("*",-1)
            }
            else if(e==="%"){
                this.decide("*",0.01)
            }
            else{
                if(! this.isPrime){
                        this.operator = this.operator ? this.operator : e
                        this.memData = this.symbolDict[this.operator](this.memData, parseFloat(this.displayData))
                        this.operator = e
                        this.displayData = this.memData.toString()
                    }
                else{
                    this.memData = parseInt(this.displayData)
                    this.isPrime = false
                    this.operator = e
                }
        }
        this.isNew = true
    }
}
}
</script>

<style scoped lang="scss">
@import "../assets/animation.scss";
@import "../assets/mixins.scss";

#container{
    display: flex;
    margin: $length / 2 $length * 4;
    justify-content: space-around;
    align-items: center;
}
#calculator{
    border-bottom: 8px darkgrey solid;
    border-radius: 6% 6% 3% 3%;
    padding: 2%;
    background: linear-gradient(0deg, lightgrey, gainsboro);
    width: 500px;
    height: $length*8;
    display: grid;
    grid-template-areas: 
    "d d d d"
    "f f f s"
    "n n n s"
    ;
}


#display{
    grid-area: d;
}

#func-pad{
    grid-area: f;
    display: grid;
    grid-template-columns: repeat(3,1fr);
}

#num-pad{
    grid-area: n;
    display: grid;
    grid-template-columns: repeat(3,1fr);
}

#symbol-pad{
    grid-area: s;
    display: grid;
    align-content: stretch;

}

</style>
