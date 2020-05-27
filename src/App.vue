<template>
    <div id="app">
        <div id="controller">
            <button v-on:click="$refs.board.next_board()">NEXT BOARD</button>
            <button v-on:click="$refs.board.start()">START</button>
            <button v-on:click="$refs.board.pause()">PAUSE</button>
            <button v-on:click="$refs.board.reset()">RESET</button>
        </div>
        <board ref="board"></board>
    </div>
</template>

<script>
    import board from "@/components/board";

    export default {
        name: 'App',

        components: {
            board
        }
    }
</script>

<style>
    #app {
        display: flex;
        height: 100%;
        align-items: center;
        justify-content: center;
        font-family: Avenir, Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: center;
        color: #2c3e50;
        margin-top: 60px;
        background: #4c5bed;
    }

    #controller {
      display: grid;
      grid-template: repeat(4, 100px) / repeat(1, 1fr);
      border: solid;
    }
</style>
