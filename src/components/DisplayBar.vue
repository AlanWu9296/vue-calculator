<template>
    <div>
        <p>{{displayData}}</p>
    </div>
</template>

<script>
    export default {
        name:"DisplayBar",
        props:["displayData"]
    }
</script>

<style scoped lang="scss">
    @import "../assets/mixins"
</style>