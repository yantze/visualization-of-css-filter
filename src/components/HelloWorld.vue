<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <img width="35%" src="../assets/elena.jpeg" :style="styleObject">
    <div>
      <input type="text" name="imgsrc" v-model="imgSrc">
    </div>
    <div class="des" v-if="curAttrName">
      当前滚动的是 {{ curAttrName }}
    </div>
    <div class="attr" v-for="attr of filterAttrs" :key="attr.name">
      <label for="">{{ attr.name }}: {{ attr.value }} {{ attr.unit }}</label>
      <input type="range" :min="attr.start" :max="attr.end" :step="attr.step"
        class="slider" v-model="attr.value" @change="changeValue(attr)">
    </div>

  </div>
</template>
/*
    filter: contrast(1700%);
    filter: blur(3px);
    filter: brightness(1.25);
    filter: grayscale(27%);
    filter: invert(100%);
    filter: sepia(100%);
    filter: hue-rotate(180deg);
    filter: filter: opacity(50%);
*/
<script>
export default {
  name: "HelloWorld",
  data() {
    return {
      msg: "Welcome",
      curAttrName: "",
      imgSrc: "../assets/elena.jpeg",
      filterAttrs: [
        {
          name: "contrast",
          start: 1,
          end: 200,
          value: 100,
          status: "origin",
          unit: "%"
        },
        {
          name: "blur",
          start: 0,
          end: 30,
          value: 0,
          step: 0.1,
          status: "origin",
          unit: "px"
        },
        {
          name: "brightness",
          start: 0,
          end: 2,
          step: 0.1,
          value: 1,
          status: "origin",
          unit: ""
        },
        {
          name: "grayscale",
          start: 0,
          end: 200,
          value: 0,
          status: "origin",
          unit: "%"
        },
        {
          name: "invert",
          start: 0,
          end: 100,
          value: 0,
          status: "origin",
          unit: "%"
        },
        {
          name: "sepia",
          start: 0,
          end: 100,
          value: 0,
          status: "origin",
          unit: "%"
        },
        {
          name: "hue-rotate",
          start: 0,
          end: 360,
          value: 0,
          status: "origin",
          unit: "deg"
        },
        {
          name: "opacity",
          start: 0,
          end: 100,
          value: 100,
          status: "origin",
          unit: "%"
        },
        {
          name: "saturate",
          start: 0,
          end: 10,
          step: 0.1,
          value: 1,
          status: "origin",
          unit: ""
        }
      ]
    };
  },
  computed: {
    styleObject: function() {
      let changedArr = this.filterAttrs.filter(attr => {
        return attr.status !== "origin";
      });
      let changedStrArr = changedArr.map(
        attr => `${attr.name}(${attr.value}${attr.unit})`
      );

      return {
        filter: changedStrArr.join(" ")
      };
    }
  },
  methods: {
    changeValue: function(attr) {
      this.curAttrName = attr.name;
      attr.status = "changed";
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1,
h2 {
  font-weight: normal;
}

.slidecontainer {
  width: 100%;
}

.slider {
  -webkit-appearance: none;
  width: 100%;
  height: 25px;
  background: #d3d3d3;
  outline: none;
  opacity: 0.7;
  -webkit-transition: 0.2s;
  transition: opacity 0.2s;
}

.slider:hover {
  opacity: 1;
}

.slider::-webkit-slider-thumb {
  -webkit-appearance: none;
  appearance: none;
  width: 25px;
  height: 25px;
  background: #4caf50;
  cursor: pointer;
}

.slider::-moz-range-thumb {
  width: 25px;
  height: 25px;
  background: #4caf50;
  cursor: pointer;
}
</style>
