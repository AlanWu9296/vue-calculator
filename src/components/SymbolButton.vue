<template>
        <button @click="$emit('symClicked',name)">{{name}}</button>
</template>

<script>
    export default {
        name:"SymbolButton",
        props:["name"]
    }
</script>

<style scoped lang="scss">
@import "../assets/mixins";
button{
    color: black;
    background-color: orange;
    box-shadow: 0 4px 3px 0 darkorange;
}
</style>