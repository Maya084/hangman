<script lang="ts">
</script>

<main>
    <div class="person-body">
        <div class="person head" />
        <div class="person body" />
        <div class="person left-arm" />
        <div class="person right-arm" />
        <div class="person left-leg" />
        <div class="person right-leg" />
    </div>
</main>

<style>

    .person-body {
        background-color: aquamarine;
        position: relative;
        width: 200px;
        height: 400px;
    }

    .head{
        position: absolute;
        top: var(--top-person);
        border: var(--outline-width) solid var(--person-color); 
        border-radius: 50%;
        width: var(--head-size);
        height: var(--head-size);  
        left: 50%;     
        transform: translateX(-50%);
    }

    .body{
        width: var(--outline-width);
        height: var(--body-height);
        background-color: var(--person-color);

        position: absolute;
        top: calc(var(--head-size) + var(--outline-width) + var(--top-person));
        left: 50%;     
        transform: translateX(-50%);
    }

    .left-leg{
        width: var(--outline-width);
        height: var(--leg-length);
        background-color: var(--person-color);

        position: absolute;
        top: calc(var(--head-size) + var(--outline-width) + var(--top-person) + var(--body-height));
        left: 50%;     
        transform: translateX(-26px);
        rotate: 24deg;
    }

    .right-leg{
        width: var(--outline-width);
        height: var(--leg-length);
        background-color: var(--person-color);

        position: absolute;
        top: calc(var(--head-size) + var(--outline-width) + var(--top-person) + var(--body-height));
        right: 50%;     
        transform: translateX(26px);
        rotate: -24deg;
    }
</style>
