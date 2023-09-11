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
          {{ cell }}
        </div>
      </div>
    </div>
    <div class="message">
      <p>{{ message }}</p>
      <button @click="startNewGame">Reiniciar</button>
      <div style="margin-top: 10px"></div>
      <button @click="startGame">Nuevo juego</button>
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
      apiBaseUrl: "https://0h2kov0us3.execute-api.us-east-1.amazonaws.com",
      currentGameId: null,
    };
  },
  methods: {
    makeMove(row, col) {
      if (
        this.currentGameId &&
        this.board[row][col] === "" &&
        !this.isGameOver()
      ) {
        axios
          .put(`${this.apiBaseUrl}/makeMove/${this.currentGameId}`, {
            row,
            col,
          })
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
          });
      }
    },
    startGame() {
      axios
        .put(`${this.apiBaseUrl}/1`)
        .then((response) => {
          if (response.data.success) {
            // Debes asignar el ID del juego aquí
            this.currentGameId = response.data.gameId;

            this.board = [
              ["", "", ""],
              ["", "", ""],
              ["", "", ""],
            ];
            this.currentPlayer = "X";
            this.message = "";
          } else {
            console.error("Error al iniciar el juego");
          }
        })
        .catch((error) => {
          console.error(error);
        });
    },
    startNewGame() {
      if (this.currentGameId) {
        // Verifica que tengas un juego en curso
        axios
          .put(`${this.apiBaseUrl}/resetGame/${this.currentGameId}`)
          .then((response) => {
            if (response.data.success) {
              // Reinicia el juego en el frontend
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
      }
    }
  },
};
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

.message {
  margin-top: 20px;
  font-size: 1.5em;
}

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
