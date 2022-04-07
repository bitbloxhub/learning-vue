<template>
    <h1>vue.js wordle</h1>
    <div v-for="guess in guesses_shown" :key="guess">
        <p v-html="guess" class="grid" style="font-family: monospace;"></p>
    </div>
    <form class="grid" @submit.prevent="guess">
        <input type="text" v-model="current_guess" placeholder="guess" minlength="5" maxlength="5" />
        <button>guess!</button>
    </form> 
</template>

<script setup>
    /* eslint-disable */
    import { ref, computed } from "vue"

    const colors = {
        "correct": "var(--secondary)",
        "miss-correct": "var(--secondary-inverse)",
        "miss": "var(--contrast)",
        "done": "var(--primary)"
    }

    const wordlist = [
        "pinia",
        "vuejs",
        "vetur",
    ]

    const current_guess = ref("")

    const guesses = ref([])
    const guesses_left = ref(6)
    const word = wordlist[Math.floor(Math.random() * wordlist.length)]
    const done = ref(false)

    const guesses_shown = computed(() => {
        return guesses.value.map((guess) => {
            return guess.map((letter_info) => {
                return `<div style="background-color: ${colors[letter_info["correct"]]}; text-align: center;">${letter_info["letter"]}</div>`
            }).join("")
        })
    })

    function guess() {
        if (guesses_left.value != 0) {
            guesses_left.value--
            guesses.value.push([...current_guess.value].map((guess_char, index) => {
                if (word.includes(guess_char)) {
                    if (word[index] == guess_char) {
                        return {"correct": "correct", "letter": guess_char}
                    }
                    return {"correct": "miss-correct", "letter": guess_char}
                }
                return {"correct": "miss", "letter": guess_char}
            }))
        } else {
            if (done.value) {} else {
                done.value = true
                guesses.value.push([...word].map((char) => {
                    return {"correct": "done", "letter": char}
                })
            )}
        }
    }
</script>