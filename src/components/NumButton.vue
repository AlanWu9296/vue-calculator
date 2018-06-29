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
</style>