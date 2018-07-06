<template>
    <button  @click="$emit(eventName, name)">{{name}}</button>
</template>

<script>
    export default {
        name:"BaseButton",
        props:["name","timeInterval","keyCodeDict","eventName"],
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
@import "../assets/mixins.scss";
</style>
