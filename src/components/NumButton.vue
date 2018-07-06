<script>
import BaseButton from "./_Button"

    export default {
        name:"numButton",
        extends:BaseButton,
    }
</script>

<style scoped lang="scss">
button{
    box-shadow: 0 4px 3px 0 hsl(0, 0, 50);
    background-color: darkgrey;
    }

button:hover{
    color: coral;
    }

</style>