<script lang="ts">
    import { onMount } from "svelte";
    import { ShowPartsStore } from "./hangman-store";

    //word to guess
    let word = "MAJA";
    //letters that are guessed but not in the word
    let wrong = "";

    //LIST OF LETTERS
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
        //prevents playing with html disabled properties and 
        //clicking a button that is already clicked
        if (options[letter]) {
            return;
        }

        //letter is guessed
        options[letter] = true;

        //letter is present in the word
        if (word.indexOf(letter) >= 0) {
            return;
        }

        //add the letter to the wrong pile
        wrong += letter;

        //show another part of the body
        ShowPartsStore.update((currentList) => {
            return [...currentList, wrong.length];
        });
    }

    function reset() {
        //set all properties to false
        Object.keys(options).forEach((letter) => {
            options[letter] = false;
        });

        wrong = "";
    }

    onMount(() => {
        reset();
    });
</script>

<main>
    <!-- WORD TO GUESS -->
    <div class="word-container">
        {#each word.split("") as letter}
            <div class="letter">
                <span hidden={!options[letter]}>
                    {letter}
                </span>
            </div>
        {/each}
    </div>

    <!-- LETTERS -->
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
