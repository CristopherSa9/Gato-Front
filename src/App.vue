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
      apiBaseUrl: "https://46i3aj7hn3.execute-api.us-east-1.amazonaws.com",
      currentGameId: ?,
    };
  },   
}
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
