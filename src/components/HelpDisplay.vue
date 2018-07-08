<template>
    <div>
        <div id="instruction">
            <h1>Help Instructions</h1>
            <p>You can both use the mouse and keyboard to use the calculator.Use mouse to click the button for responding function and the keyboard mapping is as below:</p>
            <ul>
                <li>use number pad for 0~9 input</li>
                <li>use backspace or delete to modify</li>
                <li>use ESC to clear and reset </li>
            </ul>
        </div>
    </div>
</template>

<script>
    export default {
        name:"helper",
    }
</script>

<style scoped lang="scss">
@import "../assets/mixins.scss";
    div{
        width: $length * 8;
        height: 500px;
        left:50%;
        display: flex;
    }

    #instruction{
        display: flex;
        flex-direction: column;
        justify-content:center;
        text-align: left;
        height:auto;
        padding:20px;
        h1{
            font-family: 'Courier New', Courier, monospace;
            padding: 0;
            margin: 0;
            color: lightsalmon;
        }

        ul{
            padding: 0px 15px;
            font-size: 18px;
            color: dimgray;
        }
        p{
            color: grey;
            font-size: 15px;
        }
    }
</style>