<template>
  <div class="rhythm">
    <div class="rhythm-board">
      <h1>Rhythm</h1>
      <h1>bpm:{{ state.bpm }}</h1>
      <input type="range" min="60" max="500" v-model="state.bpm" class="slider" id="myRange" />
      <div class="controller">
        <div
          class="button"
          v-for="(element, index) in state.buttonInfo"
          :key="index"
          :class="{ buttonPlay: element.isPlay, buttonActive: element.isActive }"
          @click="toggleActive(index)"
        ></div>
      </div>
      <div class="goButton" @click="start">GO</div>
    </div>
  </div>
</template>

<script setup>
import { reactive } from 'vue';

const buttonCount = 16;
const buttonInfo = [];
const someSound = require('@/assets/c3.mp3');

const audio = new Audio(someSound); // path to file
audio.play();
for (let i = 0; i < buttonCount; i += 1) {
  buttonInfo.push({
    id: i,
    isActive: false,
    isPlay: false,
  });
}
const state = reactive({
  bpm: 120,
  buttonInfo,
});
const toggleActive = (index) => {
  state.buttonInfo[index].isActive = !state.buttonInfo[index].isActive;
};
const sleep = function sleep(ms) {
  return new Promise((resolve) => setTimeout(resolve, ms));
};
async function start() {
  for (let i = 0; i < buttonCount; i += 1) {
    state.buttonInfo[i].isPlay = true;
    if (state.buttonInfo[i].isActive) {
      if (audio.paused) {
        audio.play();
      } else {
        audio.currentTime = 0;
      }
    }
    // eslint-disable-next-line no-await-in-loop
    await sleep((60 / state.bpm) * 1000);
    state.buttonInfo[i].isPlay = false;
  }
}
// };
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.rhythm-board {
  border: 3px solid pink;
  max-width: 600px;
  // height: 800px;
  border-radius: 12px;
  padding: 20px;
  margin: 0px auto;
}
.controller {
  display: flex;
  flex-wrap: wrap;
  .button {
    width: 23%;
    height: 36px;
    background-color: #aaa;
    margin: 1%;
    margin-bottom: 30px;
    border-radius: 4px;
  }
  .button:hover {
    cursor: pointer;
    background-color: #bbb;
  }
  .buttonActive {
    background-color: yellow;
  }
  .buttonActive:hover {
    background-color: darken($color: yellow, $amount: 10);
  }
  .buttonPlay {
    background-color: purple;
  }
}
.goButton {
  color: white;
  background-color: #666;
  padding: 10px;
  &:hover {
    background-color: goldenrod;
    cursor: pointer;
  }
}
.slider {
  -webkit-appearance: none;
  width: 100%;
  height: 6px;
  background: #222;
  outline: none;
  opacity: 0.7;
  -webkit-transition: 0.2s;
  transition: opacity 0.2s;
  &:hover {
    opacity: 1;
  }
  &::-webkit-slider-thumb {
    -webkit-appearance: none;
    appearance: none;
    width: 10px;
    height: 10px;
    border-radius: 50%;
    background: #666;
    cursor: pointer;
  }

  &::-moz-range-thumb {
    width: 10px;
    height: 10px;
    border-radius: 50%;
    background: #666;
    cursor: pointer;
  }
}

h1 {
  font-size: 24px;
  color: white;
}
</style>
