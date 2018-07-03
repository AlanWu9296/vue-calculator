<template>
    <button @click="$emit('numClicked', name)">{{name}}</button>
</template>

<script>
    export default {
        name:"NumberButton",
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
    box-shadow: 0 4px 3px 0 hsl(0, 0, 50);
}

button:hover{
    color: coral;
}
</style>