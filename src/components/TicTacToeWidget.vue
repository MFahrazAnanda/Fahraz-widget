<template>
  <div class="tic-tac-toe-widget">
    <h2>Tic Tac Toe</h2>
    <div class="board">
      <div v-for="(cell, index) in board" :key="index" @click="handleClick(index)" :class="getCellClass(cell)">
        {{ cell }}
      </div>
    </div>
    <p :class="statusClass">{{ status }}</p>
    <button @click="resetGame">Permainan Baru</button>
  </div>
  <p v-if="isGameEnded && winner" class="winner">Pemain {{ winner }} Menang!</p>
</template>

<script>
export default {
  data() {
    return {
      board: ['', '', '', '', '', '', '', '', ''],
      currentPlayer: 'X',
      isGameEnded: false,
    };
  },
  computed: {
  status() {
    if (this.isGameEnded) {
      if (this.board.includes('')) {
        return `Pemain ${this.currentPlayer} Menang!`;
      } else {
        return 'Permainan Berakhir, Hasil Seri!';
      }
    }
    return `Giliran Pemain (${this.currentPlayer})`;
  },
},
  methods: {
    handleClick(index) {
      if (!this.isGameEnded && this.board[index] === '') {
        this.board[index] = this.currentPlayer;
        this.checkWinner();
        this.currentPlayer = this.currentPlayer === 'X' ? 'O' : 'X';
      }
    },
    checkWinner() {
      const winningCombinations = [
        [0, 1, 2],
        [3, 4, 5],
        [6, 7, 8],
        [0, 3, 6],
        [1, 4, 7],
        [2, 5, 8],
        [0, 4, 8],
        [2, 4, 6],
      ];

      for (const combination of winningCombinations) {
        const [a, b, c] = combination;
        if (
          this.board[a] &&
          this.board[a] === this.board[b] &&
          this.board[a] === this.board[c]
        ) {
          this.isGameEnded = true;
          this.status = `Pemain ${this.currentPlayer} Menang!`;
          return;
        }
      }
      if (!this.board.includes('')) {
        this.isGameEnded = true;
        this.status = 'Permainan Berakhir, Hasil Seri!';
      }
    },
    resetGame() {
      this.board = ['', '', '', '', '', '', '', '', ''];
      this.currentPlayer = 'X';
      this.isGameEnded = false;
    },
    getCellClass(cell) {
      if (cell === 'X') {
        return 'x';
      } else if (cell === 'O') {
        return 'o';
      }
      return '';
    },
  },
};
</script>

<style scoped>
.tic-tac-toe-widget {
  width: 700px;
  height: 600px;
  margin: 0 auto;
  font-size: 20px;
  border: 3px solid #333;
  border-radius: 25px;
  padding: 20px;
  margin-bottom: 20px;
  text-align: center;
  background-color: #f2f2f2;
}

.board {
  display: inline-grid;
  grid-template-columns: repeat(3, 1fr);
  grid-gap: 10px;
  margin-bottom: 20px;
}

.board div {
  border: 3px solid #333;
  width: 75px;
  height: 75px;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  padding: 5px;
}

.board div.x {
  color: #ff0000;
  font-size: 50px; 
  font-style: bold;
}

.board div.o {
  color: #0000ff;
  font-size: 50px;
  font-style: bold;
}

button {
  margin-top: 50px;
  display: block;
  margin: 0 auto; 
  background-color: #ff0000;
  color: #ffffff; 
  font-size: 18px; 
  padding: 10px 20px; 
  border-radius: 5px;
}

p {
  text-align: center;
}

p .winner {
  font-size: 24px;
  font-weight: bold;
  color: #00ff00;
  margin-top: 20px;
}

</style>