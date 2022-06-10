<script>
    export let text;
</script>

<div class="header">
    <h1>{text}</h1>
</div>

<style>
    .header {
        height: 150px;
        width: 100%;
        display: flex;
        align-items: center;
        background-image: linear-gradient(
        45deg,
        hsl(240deg 100% 20%) 0%,
        hsl(304deg 100% 23%) 22%,
        hsl(329deg 100% 36%) 42%,
        hsl(346deg 83% 51%) 60%,
        hsl(17deg 100% 59%) 76%,
        hsl(40deg 100% 50%) 89%,
        hsl(55deg 100% 50%) 100%
        );  
    }

    .header > h1 {
        text-align: center;
        width: 100%;
        font-family: "Bebas Neue", cursive;
        font-size: 50px;
    }

</style>