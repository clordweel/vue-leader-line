<template>
  <polyline
    :points="points"
    :style="`fill: none; stroke: ${color}; stroke-width: ${thickness}`"
  />
</template>

<script>
export default {
  name: "VerticalLeaderLine",
  props: {
    color: { type: String, default: "currentColor" },
    thickness: { type: Number, default: 3 },

    /* [start, end] */
    start: Array,
    /* [start, end] */
    end: Array,
    /* [start, end] */
    padding: Array,
  },

  computed: {
    points() {
      const { start, end, padding } = this.$props;

      const [lsx = 0, lsy = 0] = start;
      const [lex = 0, ley = 0] = end;
      const [sp = 0, ep = 0] = padding;

      const [_1, _2, _3, _4] = [
        `${lsx},${lsy}`,
        `${lsx + sp},${lsy}`,
        `${lex - ep},${ley}`,
        `${lex},${ley}`,
      ];

      return `${_1} ${_2} ${_3} ${_4}`;
    },
  },
};
</script>
