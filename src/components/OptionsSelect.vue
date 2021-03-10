<template>
  <div class="custom-select">
    <select v-model="state.categorySelected" @change="choseCat">
      <option disabled value="">Choose a category</option>
      <option
        :value="category"
        v-for="(category, i) in state.options.categories"
        :key="i"
      >
        {{ category }}
      </option>
    </select>
  </div>
  <div class="custom-select">
    <select v-model="state.levelSeleted" @change="choseLevel">
      <option disabled value="">Choose a level</option>
      <option value="0">Easy</option>
      <option value="1">Medium</option>
      <option value="2">Hard</option>
    </select>
  </div>
</template>

<script>
import { reactive } from "vue";

import options from "../assets/options";

export default {
  name: "OptionsSelect",
  setup(props, context) {
    const state = reactive({
      options: options,
      categorySelected: "",
      levelSeleted:""
    });

    function choseCat(cat) {
      let value = cat.target.value;
      context.emit("category-chosen", value);
    }

    function choseLevel(level) {
        let value = level.target.value;
        context.emit("level-chosen", value);
    }

    return {
      state,
      choseCat,
      choseLevel
    };
  },
};
</script>

<style scoped lang="scss">
$height: 2rem;
$color: #ff1744;
.custom-select {
  position: relative;
  width: $height * 6;
  height: $height;
  background-color: #fff;
  border-radius: 5px;
  &:after {
    content: "▽";
    font-weight: 900;
    position: absolute;
    top: 0;
    right: 0;
    color: $color;
    width: $height/2;
    height: $height/2;
    transform: translate(-50%, 50%);
    z-index: 1;
  }
  select {
    width: 100%;
    height: 100%;
    background-color: transparent;
    color: $color;
    border: none;
    outline: none;
    padding: 0 $height/2;
    appearance: none;
    position: relative;
    z-index: 2;
  }
}
</style>