<template>
  <div id="tic_tac_toe-component">
    <!-- Rows -->
    <div v-for="(columns, row) in rows" :key="row">
      <!-- Columns -->
      <span v-for="(player, column) in columns" :key="column">
        <!-- Cell -->
        <cell
          class="cell"
          :player="player"
          @click.native="cellClick(row, column)"
        />
      </span>
    </div>

    <div id="info-wrapper">
      <!-- Player Active -->
      <span id="player-active"
        >Turn: <b>{{ player_active }}</b></span
      >
      <!-- Reset Game Button -->
      <span id="btn-reset" @click="resetGame">Reset</span>
    </div>
  </div>
</template>

<script>
import Cell from '@/components/cell';

export default {
  components: {
    cell: Cell
  },
  data() {
    return {
      rows: [['', '', ''], ['', '', ''], ['', '', '']],
      players: ['O', 'X'],
      player_active: 'O',
      game_end: false,
      winner: null,
      cell_click: 0
    };
  },
  methods: {
    resetGame() {
      this.winner = null;
      this.game_end = false;
      this.cell_click = 0;
      this.player_active = 'O';
      this.rows = [['', '', ''], ['', '', ''], ['', '', '']];
    },
    cellClick(row, column) {
      if (
        this.game_end ||
        this.cell_click == 9 ||
        this.rows[row][column] !== ''
      )
        return;
      this.cell_click += 1;

      // Set cell player
      this.$set(this.rows[row], column, this.player_active);
      // Calculate if column match
      this.calculate(row, column, this.player_active);
      // Change player active
      this.changePlayerActive();
      // If the game draw
      if (this.cell_click == 9 && this.game_end === false) {
        alert('The Game Draw!!');
      }
    },
    changePlayerActive() {
      this.player_active == 'O'
        ? (this.player_active = 'X')
        : (this.player_active = 'O');
    },
    setWinner() {
      this.game_end = true;
      this.winner = this.player_active;
      alert(`Game End!! The winner is ${this.winner}`);
    },
    calculate(row, column) {
      if (row == 1 && column == 1) {
        // Di paling tengah
        this.checkColumn(this.rows[row]);
        this.checkRows(column);

        for (let i = 0; i <= 2; i += 2) {
          for (let j = 0; j <= 2; j += 2) {
            if (this.game_end === true) return;
            this.checkCross(i, j);
          }
        }
      } else if ([0, 2].includes(row) && [0, 2].includes(column)) {
        // Di Samping
        this.checkColumn(this.rows[row]);
        this.checkRows(column);
        this.checkCross(row, column);
      } else {
        // Di tengah
        this.checkColumn(this.rows[row]);
        this.checkRows(column);
      }
    },
    checkRows(column) {
      // Iterate and check if the player !== player_active
      // then go out from this function
      for (const row of this.rows) {
        if (row[column] !== this.player_active) return;
      }

      // Set winner
      this.setWinner();
    },
    checkColumn(players) {
      // Iterate and check if the player !== player_active
      // then go out from this function
      for (const player of players) {
        if (player !== this.player_active) return;
      }

      // Set winner
      this.setWinner();
    },
    checkCross(row, column) {
      if (row == 2) column == 0 ? (column = 2) : (column = 0);

      let i = column;
      for (const row of this.rows) {
        if (row[i] !== this.player_active) return;

        column == 0 ? i++ : i--;
      }

      // Set Winner
      this.setWinner();
    }
  }
};
</script>

<style scoped>
.cell {
  display: inline-block;
  border: 4px solid #494747c7;
}

#info-wrapper {
  text-align: center;
  width: 50%;
  margin: 30px auto;
}

#player-active {
  margin-right: 39px;
  background-color: white;
  padding: 10px;
  border-radius: 4px;
}

@media only screen and (min-width: 426px) {
  #player-active {
    margin-right: 50px;
  }
}

@media only screen and (min-width: 686px) {
  #player-active {
    margin-right: 180px;
  }
}

#btn-reset {
  padding: 10px 20px;
  color: white;
  background-color: red;
  border-radius: 4px;
  cursor: pointer;
  box-shadow: 6px 8px 4px #e424249f;
}
</style>
