<script lang="ts">
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
        if(word.indexOf(letter)>=0){
            return
        }

        wrong += letter;
        ShowPartsStore.update((currentList) => {
            return [...currentList, wrong.length];
        })
    }
</script>

<main>
    <div class="word-container">
        {#each word.split("") as letter}
            <div class="letter">{letter}</div>
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
