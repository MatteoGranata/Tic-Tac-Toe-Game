<script setup>
import { ref } from 'vue';

const rules = ref(true)

const props = defineProps({
    msg: String
})

function hide() {
    rules.value = !rules.value
}
</script>

<template>
    <div class="container-rules" @click="hide" v-if="rules">
        <div class="rules">
            <h1 class="title">rules</h1>
            <p class="explanation"> tic tac toe is a tabletop game for two players on a 3x3 grid. players use the symbols
                'x' and 'o' and take turns making moves. the objective is to achieve a row of three identical symbols
                horizontally, vertically, or diagonally. the player who accomplishes this wins the game. the game ends in a
                draw if all cells are occupied without any player achieving a winning row. it starts with <span
                    class="player"> {{ msg }} </span>
            </p>
        </div>
    </div>
</template>

<style scoped>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}


body {
    width: 100vw;
    height: 100vh;
    margin: 0;
    font-family: 'Major Mono Display', monospace;
    background: #0D0D0D;
    color: #e4dfd9;
}

.container-rules {
    display: flex;
    justify-content: center;
    align-items: center;
    position: absolute;
    top: 0;
    width: 100%;
    height: 100%;
    backdrop-filter: blur(8px);
}

.title {
    margin-top: 5%;
}

.rules {
    width: 30vw;
    height: 60%;
    backdrop-filter: blur(7px);
    box-shadow: #0d0d0d1f 10px 10px 30px;
    border-radius: 30px;
    background-color: #e4dfd906;
    justify-content: center;
}

.explanation {
    text-align: center;
    padding: 5%;
    font-size: 2.5vh;
    line-height: 3.1vh;
}

@media (max-width: 450px) {
    .rules {
        width: 90%;
        height: 70%;
    }

    .explanation {
        font-size: 2vh;
    }
}
</style>