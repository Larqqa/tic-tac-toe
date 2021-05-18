<template>
  <div>
    <p v-if="winner" class="turn">{{turn}} wins!</p>
    <p v-else class="turn">{{turn}}'s turn</p>

    <div class="board">
      <button v-for="(n, i) in board" :key="i" v-on:click="toggleBoard(i)" class="space" :disabled="winner">{{n}}</button>
    </div>

    <button v-if="winner" v-on:click="resetBoard">Reset?</button>
  </div>
</template>

<script>
export default {
  name: 'Board',
  data: function() {
    return {
      turn: 'O',
      winner: false,
      board: Array.from({length: 9})
    };
  },
  methods: {
    resetBoard: function() {
      this.board = Array.from({length: 9});
      this.winner = false;
      this.turn = 'O';
    },
    checkRows: function(turn) {
      for (let i = 0; i < 9; i += 3) {
        if (this.board[0 + i] === turn && this.board[1 + i] === turn && this.board[2 + i] === turn) return true;
      }
      for (let i = 0; i < 3; i++) {
        if (this.board[0 + i] === turn && this.board[3 + i] === turn && this.board[6 + i] === turn) return true;
      }

      if (this.board[0] === turn && this.board[4] === turn && this.board[8] === turn) return true;
      if (this.board[6] === turn && this.board[4] === turn && this.board[2] === turn) return true;

      return false;
    },
    toggleBoard: function(n) {
      if (!this.board[n]) {
        this.board[n] = this.turn;

        if (this.checkRows(this.turn)) {
          this.winner = true;
        } else {
          if (this.turn === 'O') this.turn = 'X';
          else if (this.turn === 'X') this.turn = 'O';

          if (this.board.filter(x => !x).length === 0) {
            this.turn = 'No one';
            this.winner = true;
          }
        }
      }
    }
  }
}
</script>

<style scoped>
.turn {
  text-align: center;
}

.board {
  display: flex;
  flex-wrap: wrap;
  width: 150px;
  height: 150px;
}

.space {
  width: 33.3333%;
  height: 33.3333%;
}
</style>