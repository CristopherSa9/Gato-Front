<template>
  <div id="app">
    <h1>Tic Tac Toe</h1>
    <div class="board">
      <div v-for="(row, rowIndex) in board" :key="rowIndex" class="row">
        <div
          v-for="(cell, colIndex) in row"
          :key="colIndex"
          class="cell"
          @click="makeMove(rowIndex, colIndex)"
        >
<<<<<<< HEAD
=======
          {{ cell }}
>>>>>>> 7dd76f870a68e973906a4fc693f9c4500d3c0dc3
        </div>
      </div>
    </div>
    <div class="message">
      <p>{{ message }}</p>
<<<<<<< HEAD
      <button @click="startNewGame">Reiniciar</button>
      <div style="margin-top: 10px"></div>
      <button @click="startGame">Nuevo juego</button>
=======
      <button @click="startNewGame">Nuevo Juego</button>
>>>>>>> 7dd76f870a68e973906a4fc693f9c4500d3c0dc3
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      board: [
        ["", "", ""],
        ["", "", ""],
        ["", "", ""],
      ],
      currentPlayer: "X",
      message: "",
<<<<<<< HEAD
      apiBaseUrl: "https://46i3aj7hn3.execute-api.us-east-1.amazonaws.com",
      currentGameId: ?,
    };
  },   
}
=======
      apiBaseUrl: "http://127.0.0.1:3000", // Cambia a la URL de tu API
    };
  },
  methods: {
    makeMove(row, col) {
      if (this.board[row][col] === "" && !this.isGameOver()) {
        axios
          .post(`${this.apiBaseUrl}/makeMove`, { row, col })
          .then((response) => {
            if (response.data.success) {
              this.board[row][col] = this.currentPlayer;
              if (this.checkWinner(row, col)) {
                this.message = `¡El jugador ${this.currentPlayer} ha ganado!`;
              } else if (this.isBoardFull()) {
                this.message = "¡Es un empate!";
              } else {
                this.currentPlayer = this.currentPlayer === "X" ? "O" : "X";
              }
            } else {
              console.error(response.data.error);
            }
          })
          .catch((error) => {
            console.error(error);
            // Agregar manejo de errores adicional según sea necesario
          });
      }
    },
    checkWinner(row, col) {
      const player = this.currentPlayer;
      return (
        this.checkRow(row, player) ||
        this.checkColumn(col, player) ||
        this.checkDiagonals(player)
      );
    },
    checkRow(row, player) {
      for (let i = 0; i < 3; i++) {
        if (this.board[row][i] !== player) {
          return false;
        }
      }
      return true;
    },
    checkColumn(col, player) {
      for (let i = 0; i < 3; i++) {
        if (this.board[i][col] !== player) {
          return false;
        }
      }
      return true;
    },
    checkDiagonals(player) {
      return (
        (this.board[0][0] === player &&
          this.board[1][1] === player &&
          this.board[2][2] === player) ||
        (this.board[0][2] === player &&
          this.board[1][1] === player &&
          this.board[2][0] === player)
      );
    },
    isBoardFull() {
      for (let i = 0; i < 3; i++) {
        for (let j = 0; j < 3; j++) {
          if (this.board[i][j] === "") {
            return false;
          }
        }
      }
      return true;
    },
    isGameOver() {
      return this.message !== "";
    },
    startNewGame() {
      axios
        .post(`${this.apiBaseUrl}/resetGame`)
        .then((response) => {
          if (response.data.success) {
            // Reiniciar el juego en el frontend
            this.board = [
              ["", "", ""],
              ["", "", ""],
              ["", "", ""],
            ];
            this.currentPlayer = "X";
            this.message = "";
          } else {
            console.error("Error al reiniciar el juego");
          }
        })
        .catch((error) => {
          console.error(error);
          // Agregar manejo de errores adicional según sea necesario
        });
    },
  },
};
>>>>>>> 7dd76f870a68e973906a4fc693f9c4500d3c0dc3
</script>

<style scoped>
#app {
  text-align: center;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  margin-top: 30px;
}

.board {
  display: inline-block;
  border: 2px solid #333;
}

.row {
  display: flex;
}

.cell {
  width: 100px;
  height: 100px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 2em;
  cursor: pointer;
  border: 1px solid #ccc;
}

<<<<<<< HEAD
=======
.message {
  margin-top: 20px;
  font-size: 1.5em;
}

>>>>>>> 7dd76f870a68e973906a4fc693f9c4500d3c0dc3
button {
  font-size: 1em;
  padding: 10px 20px;
  background-color: #007bff;
  color: white;
  border: none;
  cursor: pointer;
  margin-top: 10px;
}

button:hover {
  background-color: #0056b3;
  transition: background-color 0.3s ease; /* Agregado para efecto de transición */
}
</style>
