<template>
  <div class="game-tile-container" @click="clickedTile">
    <p class="game-tile-content"
      :class="{ 'game-tile-hidden': isContentHidden }">{{ tileContent }}</p>&nbsp;
  </div>
</template>

<script>
export default {
  name: 'GameTile',
  props: ['tileContent'],
  data() {
    return {
      isContentHidden: true,
    };
  },
  methods: {
    clickedTile() {
      // eslint-disable-next-line
      alert(`clicked tile: ${this.tileContent}`);
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.game-tile-content {
  color: white;
}

.game-tile-hidden {
  display: none;
}

.game-tile-container {
  display: inline-block;
  width: 60px;
  height: 60px;
  margin: 16px;
  background: magenta;
  border-width: 2px;
  border-style: dotted;
  border-color: black;
}
</style>
