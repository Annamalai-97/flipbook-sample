<template>
  <div id="app">
    <Flipbook
      class="flipbook"
      :pages="pages"
      :pagesHiRes="pagesHiRes"
      v-slot="flipbook"
      ref="flipbook"
    >
      <div class="action-bar">
        <font-awesome-icon
          class="btn left"
          :class="{ disabled: !flipbook.canFlipLeft }"
          icon="chevron-circle-left"
          size="lg"
          @click="flipbook.flipLeft"
        ></font-awesome-icon>
        <font-awesome-icon
          class="btn plus"
          :class="{ disabled: !flipbook.canZoomIn }"
          icon="plus-circle"
          size="lg"
          @click="flipbook.zoomIn"
        ></font-awesome-icon>
        <span class>Page&nbsp;</span>
        <span class>{{ flipbook.page }}</span>
        <span class>&nbsp;of&nbsp;</span>
        <span class>{{ flipbook.numPages }}</span>
        <font-awesome-icon
          class="btn minus"
          :class="{ disabled: !flipbook.canZoomOut }"
          icon="minus-circle"
          size="lg"
          @click="flipbook.zoomOut"
        ></font-awesome-icon>
        <font-awesome-icon
          class="btn right"
          :class="{ disabled: !flipbook.canFlipRight }"
          icon="chevron-circle-right"
          size="lg"
          @click="flipbook.flipRight"
        ></font-awesome-icon>
      </div>
    </Flipbook>
  </div>
</template>

<script>
import Flipbook from "flipbook-vue";

export default {
  name: "App",
  components: {
    Flipbook
  },
  data() {
    return {
      pages: [
        null,
        "give you url here",
      ],
      pagesHiRes: [
        null,
        "give you url here",
      ]
    };
  },
  mounted() {
    window.addEventListener("keydown", function(ev) {
      let flipbook = this.$refs.flipbook;
      // return unless flipbook
      if (ev.keyCode === 37 && flipbook.canFlipLeft) {
        flipbook.flipLeft();
      }

      if (ev.keyCode === 39 && flipbook.canFlipRight) {
        flipbook.flipRight();
      }
      //flipbook.flipLeft() if ev.keyCode == 37 and flipbook.canFlipLeft
      //flipbook.flipRight() if ev.keyCode == 39 and flipbook.canFlipRight
    });
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  height: 95vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  /* background-color: #333; */
  color: #ccc;
  overflow: hidden;
}
.action-bar {
  display: flex;
  justify-content: center;
  align-items: center;
}

.action-bar .btn {
}
.action-bar .btn svg {
  bottom: 0;
}
.action-bar .btn:not(:first-child) {
  margin-left: 10px;
}
.has-mouse .action-bar .btn:hover {
  color: #ccc;
  filter: drop-shadow(1px 1px 5px #000);
  cursor: pointer;
}
.action-bar .btn:active {
  filter: none !important;
}
.action-bar .btn.disabled {
  color: #666;
  pointer-events: none;
}
.flipbook {
  width: 90vw;
  height: 90vh;
}

.flipbook .viewport {
  margin-top:10px;
  width: 90vw;
  height: calc(100vh - 50px - 40px);
}

.flipbook .bounding-box {
  box-shadow: none;
}
</style>
