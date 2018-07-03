<template >
    <div id="container" >
        <display-bar :displayData="displayData" id="display"/>
        <div id="func-pad">
            <base-button v-for="item in symbols.slice(0,3)" :key="item.id" :name="item" :timeInterval="150" :keyCodeDict="codeDict" :eventName="'symClicked'" @symClicked="handleSymbol($event)"/>
        </div>
        <div id="num-pad">
            <base-button v-for="num in numbers" :key="num" :name="num" :timeInterval="150" :keyCodeDict="codeDict" :eventName="'numClicked'" @numClicked="changeDisplay($event)"/>
        </div>
        <div id="symbol-pad">
            <base-button v-for="item in symbols.slice(3,10)" :key="item.id" :name="item" :timeInterval="150" :keyCodeDict="codeDict" :eventName="'symClicked'" @symClicked="handleSymbol($event)"/>
        </div>
    </div>
</template>

<script>
const _ = require('lodash')
import DisplayBar from "./DisplayBar"
import BaseButton from "./_Button"

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
                symbols,
                symbolDict,
                codeDict,
                displayData:"",
                isNew:true,
                isPrime:true,
                memData: null,
                operator: null,
            }
        },
        components:{
            DisplayBar,
            BaseButton,
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
#container{
    border-bottom: 8px darkgrey solid;
    border-radius: 6% 6% 3% 3%;
    padding: 2%;
    background: linear-gradient(0deg, lightgrey, gainsboro);
    margin: 0 auto;
    width: 25%;
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
    button{
        color: black;
        background-color: sandybrown;
        box-shadow: 0 4px 3px 0 peru;
    }

    button:hover{
        color: FIREBRICK;
    }
}

#num-pad{
    grid-area: n;
    display: grid;
    grid-template-columns: repeat(3,1fr);
    button{
        box-shadow: 0 4px 3px 0 hsl(0, 0, 50);
    }
    button:hover{
            color: coral;
        }
    };

#symbol-pad{
    grid-area: s;
    display: grid;
    align-content: stretch;
    button{
        color: black;
        background-color: sandybrown;
        box-shadow: 0 4px 3px 0 peru;
    }

    button:hover{
        color: FIREBRICK;
    }
}
</style>
