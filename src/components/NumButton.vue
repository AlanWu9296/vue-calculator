<template>
    <button @click="$emit('numClicked', name)">{{name}}</button>
</template>

<script>
import BaseButton from './_Button'
    export default {
        name:"NumberButton",
        props:["name","timeInterval","keyCodeDict"],
        extends:{
            mixins:[BaseButton]
        }
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