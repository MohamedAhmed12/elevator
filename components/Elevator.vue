<template>
  <div class="elevator-container">
    <div>
      <img src="~/assets/elevator.png" width="40" height="40" />
      <span> {{ number }}</span>
    </div>
  </div>
</template>

<script>
export default {
  name: "Elevator",

  props: {
    number: {
      type: Number,
      default: 1,
    },
  },
};
</script>

<style scoped>
.elevator-container {
}
.elevator-container div {
  position: relative;
  margin: 0px 10px;
}
img {
  margin-bottom: 25px;
}
span {
  position: absolute;
  bottom: 0;
  left: 35%;
}
</style>
