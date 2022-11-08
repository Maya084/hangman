<script lang="ts">
    import { onMount } from "svelte";
    import { ShowPartsStore } from "./hangman-store";

    let word = "MAJA";
    let guessed = "";
    let wrong = "";

    $: options = {
        A: false, //guessed
        B: false,
        C: false,
        D: false,
        E: false,
        F: false,
        G: false,
        H: false,
        I: false,
        J: false,
        K: false,
        L: false,
        M: false,
        N: false,
        O: false,
        P: false,
        Q: false,
        R: false,
        S: false,
        T: false,
        U: false,
        V: false,
        W: false,
        X: false,
        Y: false,
        Z: false,
    };

    function guessLetter(letter: string) {
        if (guessed.indexOf(letter) >= 0) {
            return;
        }
        options[letter] = true;
        guessed += letter;
        if (word.indexOf(letter) >= 0) {
            return;
        }

        wrong += letter;
        ShowPartsStore.update((currentList) => {
            return [...currentList, wrong.length];
        });
    }

    function reset() {
        Object.keys(options).forEach((letter) => {
            options[letter] = false;
        });
        guessed = "";
        wrong = "";
    }

    onMount(() => {
        reset();
    });
</script>

<main>
    <div class="word-container">
        {#each word.split("") as letter}
            <div class="letter">
                <span hidden={!guessed.includes(letter)}>
                    {letter}
                </span>
            </div>
        {/each}
    </div>

    <div class="guess-container">
        {#each Object.keys(options) as letter}
            <button
                class="guess-letter"
                on:click={guessLetter(letter)}
                disabled={options[letter]}><span>{letter}</span></button
            >
        {/each}
    </div>
</main>

<style>
    .word-container {
        display: flex;
        flex-wrap: wrap;
        gap: 1em;
        padding: 1em;
    }

    .letter {
        width: 50px;
        height: 50px;
        border-bottom: 5px solid;

        display: flex;
        justify-content: center;
        align-items: center;
    }
    .guess-container {
        display: flex;
        flex-wrap: wrap;
        gap: 1em;
        padding: 1em;
    }

    .guess-letter {
        all: unset;
        width: 50px;
        height: 50px;
        border-radius: 5px;
        background-color: #d4b2b2;

        display: flex;
        justify-content: center;
        align-items: center;
    }

    .guess-letter:hover {
        background-color: #d39292;
        cursor: pointer;
    }

    .guess-letter:disabled {
        background-color: #685868;
        cursor: default;
    }
</style>
