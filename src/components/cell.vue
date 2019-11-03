<template>
  <div id="cell-component">
    <!-- Cell -->
    <span class="cell">
      <!-- Player 1 Draw -->
      <div class="p1" v-if="player == 'O'">
        <div class="white-cricle" />
      </div>

      <!-- Player 2 Draw -->
      <div class="p2" v-else-if="player == 'X'">X</div>
    </span>
  </div>
</template>

<script>
export default {
  props: {
    player: {
      type: String,
      required: true
    }
  }
};
</script>

<style scoped>
.cell {
  vertical-align: top;
  width: 120px !important;
  height: 120px !important;
  text-align: center;
}

.p1 {
  margin: 15px;
  width: 90px;
  height: 90px;
  position: relative;
  border-radius: 50%;
  background-color: red;
}

.p1 .white-cricle {
  width: 70px;
  height: 70px;
  border-radius: 50%;
  background-color: #367588;
  position: absolute;
  top: 10px;
  left: 10px;
}

.p2 {
  font-size: 90px;
  font-weight: bold;
  text-align: center;
  margin-top: 9px;
  color: #05d805;
}
</style>
