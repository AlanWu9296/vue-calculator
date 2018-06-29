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
</style>