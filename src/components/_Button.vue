<template>
    <button @click="$emit(eventName, name)">{{name}}</button>
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
@import '../assets/mixins.scss';
button {
    padding: 0;
    height: $length;
    border: none;
    outline: none;
    background-color: $backgroundColor;
    margin: $margin;
    font-size: $font-height;
    display: block;
    color: $font-color;
    border-radius: $radius;
}

button:active {
    box-shadow: 0 0px 0px 0 hsla(0, 0, 0, 0.2);
}

.active {
    box-shadow: 0 0px 0px 0 hsla(0, 0, 0, 0.2);
}
</style>