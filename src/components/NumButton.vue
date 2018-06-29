<template>
    <button @click="$emit('numClicked', name)" >{{name}}</button>
</template>

<script>
    export default {
        name:"NumberButton",
        props:["name"]
    }
</script>

<style scoped lang="scss">
@import "../assets/mixins";
button{
    box-shadow: 0 4px 3px 0 hsl(0, 0, 20);
}
</style>