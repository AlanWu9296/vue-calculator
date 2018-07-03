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
@import "../assets/mixins";
$padding : 10px;
div {
    height: $length;
    text-align: left;
    text-overflow: clip;
    margin:$length / 3 10px;
    box-shadow: inset 0 4px 6px 0 hsla(0, 0, 0, 0.2);
    background: linear-gradient(0deg, mintcream, white);
}
p{
    font-size: $length - $padding;
    width: 450px;
    padding-left: 10px;
    margin: 0;
    padding-top: $padding;
    color: dimgray;
    overflow:hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
}
</style>