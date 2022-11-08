<script lang="ts">
    import { bodyParts } from "./conts";

    export let showTheseParts = [1, 2, 3];
    $: shownBodyParts = bodyParts.filter((el)=>showTheseParts.includes(el.order));
</script>

<main>
    <div class="person-body">
        {#each shownBodyParts as bodyPart}
            <div class="person {bodyPart.name}" hidden={bodyPart.hidden} />
        {/each}
    </div>
</main>

<style>
    .person-body {
        background-color: aquamarine;
        position: relative;
        width: 200px;
        height: 400px;
    }

    .head {
        position: absolute;
        top: var(--top-person);
        border: var(--outline-width) solid var(--person-color);
        border-radius: 50%;
        width: var(--head-size);
        height: var(--head-size);
        left: 50%;
        transform: translateX(-50%);
    }

    .body {
        width: var(--outline-width);
        height: var(--body-height);
        background-color: var(--person-color);

        position: absolute;
        top: calc(var(--head-size) + var(--outline-width) + var(--top-person));
        left: 50%;
        transform: translateX(-50%);
    }

    .left-leg {
        width: var(--outline-width);
        height: var(--leg-length);
        background-color: var(--person-color);

        position: absolute;
        top: calc(
            var(--head-size) + var(--outline-width) + var(--top-person) +
                var(--body-height)
        );
        left: 50%;
        transform: translateX(-26px);
        rotate: 24deg;
    }

    .right-leg {
        width: var(--outline-width);
        height: var(--leg-length);
        background-color: var(--person-color);

        position: absolute;
        top: calc(
            var(--head-size) + var(--outline-width) + var(--top-person) +
                var(--body-height)
        );
        right: 50%;
        transform: translateX(26px);
        rotate: -24deg;
    }

    .left-arm {
        width: var(--outline-width);
        height: var(--arm-length);
        background-color: var(--person-color);

        position: absolute;
        top: calc(
            var(--head-size) + var(--outline-width) + var(--top-person) +
                calc(var(--body-height) / 4)
        );
        left: 50%;
        transform: translateX(-26px);
        rotate: 24deg;
    }

    .right-arm {
        width: var(--outline-width);
        height: var(--arm-length);
        background-color: var(--person-color);

        position: absolute;
        top: calc(
            var(--head-size) + var(--outline-width) + var(--top-person) +
                calc(var(--body-height) / 4)
        );
        right: 50%;
        transform: translateX(26px);
        rotate: -24deg;
    }
</style>
