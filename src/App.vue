<template>
  <div id="app">
    <div class="start" ref="start">START</div>
    <div class="end" ref="end">END</div>

    <leader-line constraint ref="z" />
  </div>
</template>

<script>
  import LeaderLine from "./";

  export default {
    name: "App",
    components: {
      LeaderLine,
    },
    mounted() {
      this.$refs.z.binds(this.$refs.start, this.$refs.end);
    },
  };
</script>

<style>
  .start,
  .end {
    border: 1px solid #000;
    height: 2em;
    justify-content: center;
    align-items: center;
    display: flex;
  }
  .start {
    width: 4em;
    margin-top: 40px;
    margin-left: 30px;
  }
  .end {
    width: 3em;
    margin-top: 240px;
    margin-left: 300px;
  }
</style>