<template>
  <div class="container">
    <Elevator
      v-for="(elevator, index) in elevators"
      :key="index"
      :number="index + 1"
      ref="elevators"
      :class="`elevetor-${index + 1}`"
    />

    <div class="building">
      <Floor
        v-for="(floor, index) in floors"
        :key="index"
        :index="index"
        @callElevator="callElevator"
      />
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      floors: 20,
      elevators: 3,
      elevatorFloorDistanceDiff: [],
      elevatorPositions: [
        {
          number: 1,
          distance: "10px",
        },
        {
          number: 2,
          distance: "10px",
        },
        {
          number: 3,
          distance: "10px",
        },
      ],
    };
  },

  methods: {
    callElevator(e) {
      this.detectElevatorsCoordinate(e);
      let nearestElevator = this.findNearestElevator();
      this.moveElevator(e, nearestElevator.number);
    },
    detectElevatorsCoordinate(floorCoordinates) {
      // change the refrenced dom Elements to offsetTop values
      this.elevatorFloorDistanceDiff = this.$refs.elevators.map(
        (elevator, index) => {
          // console.log(this.elevatorPositions[index]["distance"], index);
          return {
            number: index + 1,
            distance: Math.abs(
              parseInt(this.elevatorPositions[index]["distance"]) - floorCoordinates
            ),
          };
        }
      );
    },
    findNearestElevator() {
      // change each offsetTop value(coordinate) to the difference between elevator and selected floor
      this.elevatorFloorDistanceDiff.sort((a, b) => {
        return a.distance - b.distance;
      });
      
      return this.elevatorFloorDistanceDiff[0];
    },
    moveElevator(floorCoordinates, elevatorNum) {
      let currentPos = this.$anime({
        targets: `.elevator-container.elevetor-${elevatorNum} div`,
        translateY: floorCoordinates,
        duration: 2000,
      });

      setTimeout(() => {
        this.elevatorPositions[elevatorNum - 1] = {
          number: elevatorNum,
          distance: currentPos.animations[0].currentValue,
        };
      }, 500);
    },
  },
};
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: stretch;
  text-align: center;
  padding: 10px;
}

.building {
  display: flex;
  flex-direction: column;
}
</style>
