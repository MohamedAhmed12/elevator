<template>
  <div class="floor-container" @click="callElevator">
    <span class="person" :ref="`person_${index}`"></span>
    <span class="floor-number">{{ index + 1 }}</span>
  </div>
</template>

<script>
export default {
  name: "Floor",

  props: {
    index: {
      type: Number,
      default: 0,
    },
  },

  data() {
    return {
      person: "",
    };
  },

  mounted() {
    this.person = this.setPersonColor();
  },

  methods: {
    generateRandomColor() {
      var letters = "0123456789ABCDEF".split("");
      var color = "#";
      for (var i = 0; i < 6; i++) {
        color += letters[Math.floor(Math.random() * 16)];
      }

      return color;
    },
    setPersonColor() {
      this.$refs[`person_${this.index}`].style[
        "background-color"
      ] = this.generateRandomColor();
    },
    callElevator(event) {
      this.$emit("callElevator", event.target.offsetTop);
    },
  },
};
</script>

<style scoped>
.floor-container {
  display: flex;
  align-items: flex-end;
  width: 100%;
  min-width: 100vh;
  border: none;
  height: 60px;
  justify-content: space-between;
  border-bottom: 1px solid #000;
}
hr {
  width: 100%;
}
.person {
  height: 25px;
  width: 25px;
  border-radius: 50%;
}
/* .floor-number{
  position: absolute;
  right: 15
} */
</style>
