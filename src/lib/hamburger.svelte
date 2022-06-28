<script>
    let opened = false;
</script>




<div
    class="container"
    class:change={opened === true}
    on:click={() => (opened = !opened)}
>
    <div class="bar1" />
    <div class="bar2" />
    <div class="bar3" />
</div>





<style lang="scss">
    .container {
        cursor: pointer;
        position: absolute;
    }

    .bar1,
    .bar2,
    .bar3 {
        width: 35px;
        height: 5px;
        background-color: #333;
        margin: 6px 0;
        transition: 0.4s;
    }

    .change {
        .bar1 {
            -webkit-transform: rotate(-45deg) translate(-9px, 6px);
            transform: rotate(-45deg) translate(-9px, 6px);
        }

        .bar2 {
            opacity: 0;
        }

        .bar3 {
            -webkit-transform: rotate(45deg) translate(-8px, -8px);
            transform: rotate(45deg) translate(-8px, -8px);
        }
    }
</style>