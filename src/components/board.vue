<template>
    <div>
        <div>
            <button v-on:click="next_board()">NEXT BOARD</button>
            <button v-on:click="start()">START</button>
            <button v-on:click="pause()">PAUSE</button>
        </div>
        <div class="grid">
            <div class="row" v-for="(row, row_index) in grid" v-bind:key="row_index">
                <div v-for="(cell, column_index) in row" v-bind:key="column_index"
                     class="cell" v-bind:class="{live: cell.live}"
                     v-on:click="toggle_cell(row_index, column_index)"
                >
                </div>
            </div>
        </div>

    </div>

</template>

<script>

    export default {
        name: "grid",

        data() {
            return {
                game_interval: undefined,

                grid: Array.from(
                    {length: 50},
                    function () {
                        return Array.from(
                            {length: 50},
                            function () {
                                return {
                                    live: false
                                }
                            }
                        )
                    }
                )
            }
        },

        methods: {
            start() {
                this.game_interval = setInterval(() => {
                    this.next_board()
                }, 100);
            },

            pause() {
                clearInterval(this.game_interval);
            },


            toggle_cell(row_index, column_index) {
                this.grid[row_index][column_index].live = !this.grid[row_index][column_index].live;

            },

            next_board() {
                this.grid = this.grid.map((row, row_index) => {
                    return row.map((cell, column_index) => {
                        return this.transform({row_index, column_index});
                    })
                });
            },

            transform({row_index, column_index}) {
                return {
                    live: this.next_status({row_index, column_index})
                }
            },

            next_status({row_index, column_index}) {
                if (this.grid[row_index][column_index].live) {
                    return 2 <= this.live_neighbours({row_index, column_index}) && this.live_neighbours({
                        row_index,
                        column_index
                    }) <= 3;
                } else {
                    return this.live_neighbours({row_index, column_index}) === 3;
                }
            },

            live_neighbours({row_index, column_index}) {
                const moves = [-1, 0, +1];
                let live = 0;
                for (let row_move of moves) {
                    for (let column_move of moves) {
                        if (
                            !(row_move === 0 && column_move === 0) &&
                            this.is_live_cell({
                                row_index: row_index + row_move,
                                column_index: column_index + column_move
                            })) {
                            live += 1;
                        }
                    }
                }
                return live;
            },

            is_live_cell({row_index, column_index}) {
                return this.is_valid_index({index: row_index}) &&
                    this.is_valid_index({index: column_index}) &&
                    this.grid[row_index][column_index].live
            },

            is_valid_index({index}) {
                return 0 <= index && index < this.grid.length;
            }

        }
    }
</script>

<style scoped>
    .grid {
        display: grid;
        grid-template: repeat(50, 15px) / repeat(1, 1fr);
        gap: 3px;
    }

    .row {
        display: grid;
        grid-template: repeat(1, 15px) / repeat(50, 15px);
        gap: 3px;
    }

    .cell {
        background: white;
    }

    .live {
        background: black;
    }

</style>
