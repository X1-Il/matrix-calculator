<template>
  <div>
    <h1>Matrix Calculator</h1>
    <label>Matrix Size:</label>
    <input type="number" v-model="size" min="1" max="10" />
    <br /><br />
    <table>
      <tbody>
        <tr v-for="(row, rowIndex) in matrix">
          <td v-for="(value, colIndex) in row">
            <input type="number" v-model="matrix[rowIndex][colIndex]" />
          </td>
        </tr>
      </tbody>
    </table>
    <br /><br />
    <button @click="add">Add</button>
    <button @click="subtract">Subtract</button>
    <button @click="multiply">Multiply</button>
    <button @click="transpose">Transpose</button>
    <br /><br />
    <label>Result:</label>
    <div v-if="result">
      <table>
        <tbody>
          <tr v-for="(row, rowIndex) in result">
            <td v-for="(value, colIndex) in row">{{ result[rowIndex][colIndex] }}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      size: 3,
      matrix: [],
      result: null,
    };
  },
  mounted() {
    this.reset();
  },
  methods: {
    reset() {
      this.matrix = Array.from({ length: this.size }, () => Array.from({ length: this.size }, () => 0));
      this.result = null;
    },
    add() {
      this.result = this.matrix.map((row, rowIndex) =>
        row.map((value, colIndex) => value + this.matrix[rowIndex][colIndex])
      );
    },
    subtract() {
      this.result = this.matrix.map((row, rowIndex) =>
        row.map((value, colIndex) => value - this.matrix[rowIndex][colIndex])
      );
    },
    multiply() {
      this.result = Array.from({ length: this.size }, () => Array.from({ length: this.size }, () => 0));
      for (let i = 0; i < this.size; i++) {
        for (let j = 0; j < this.size; j++) {
          for (let k = 0; k < this.size; k++) {
            this.result[i][j] += this.matrix[i][k] * this.matrix[k][j];
          }
        }
      }
    },
    transpose() {
      this.result = this.matrix[0].map((col, colIndex) =>
        this.matrix.map((row) => row[colIndex])
      );
    },
  },
};
</script>
