<template>
  <div id="app">
    <div style="position: relative">
      <div
        class="pointEl"
        ref="start"
        style="
          background: red;
          height: 24px;
          width: 60px;
          margin-top: 50px;``
          margin-left: 40px;
        "
      >
        START
      </div>
      <div
        class="pointEl"
        ref="end"
        style="
          background: green;
          height: 24px;
          width: 140px;
          margin-top: 100px;
          margin-left: 300px;
        "
      >
        END
      </div>

      <leader-line ref="z" />
    </div>

    <vertical-leader-line
      :start="[0, 50]"
      :end="[50, 20]"
      :padding="[20, 20]"
    />
  </div>
</template>

<script>
// import LeaderLine, { VerticalLeaderLine } from "../dist/leader-line.common";
import LeaderLine, { VerticalLeaderLine } from "./";

export default {
  name: "App",
  props: {
    msg: String,
  },
  components: {
    LeaderLine: LeaderLine,
    VerticalLeaderLine,
  },
  mounted() {
    this.$refs.z.binds(this.$refs.start, this.$refs.end);
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.pointEl {
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
