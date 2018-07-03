<template>
        <button @click="$emit('symClicked',name)">{{name}}</button>
</template>

<script>
    export default {
        name:"SymbolButton",
        props:["name","timeInterval","keyCodeDict"],
        computed:{
        keyCode(){
                let parseCode = parseInt(this.name)
                if(parseCode || parseCode===0){
                    return [parseCode+48,parseCode+96]
                }else{
                    return this.keyCodeDict[this.name]
                }
            }
        },
        mounted(){
            let self = this
            document.addEventListener("keydown",function(){
                let keyCode = window.event.keyCode
                if(self.keyCode.indexOf(keyCode) != -1){
                    self.$el.setAttribute("class","active")
                    self.$el.click()
                    setTimeout(()=>self.$el.removeAttribute("class"),self.timeInterval)
                }
            })
        },
    }
</script>

<style scoped lang="scss">
@import "../assets/mixins";
button{
    color: black;
    background-color: sandybrown;
    box-shadow: 0 4px 3px 0 peru;
}

button:hover{
    color: FIREBRICK;
}
</style>