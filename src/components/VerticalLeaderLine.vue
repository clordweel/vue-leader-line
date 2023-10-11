<template>
  <svg
    xmlns="http://www.w3.org/2000/svg"
    version="1.1"
    style="overflow: visible; height: 0.1px; width: 0.1px"
  >
    <polyline
      :points="points"
      :style="`fill: none; stroke: ${color}; stroke-width: ${thickness}`"
    />
  </svg>
</template>

<script>
export default {
  name: "VerticalLeaderLine",
  props: {
    /* 线条颜色 */
    color: { type: String, default: "currentColor" },
    /* 线条粗细 */
    thickness: { type: Number, default: 3 },

    /* 垂线起始坐标：[start, end] */
    start: Array,
    /* 垂线结束坐标：[start, end] */
    end: Array,
    /* 起始结束点位距离两边的边距：[start, end] */
    padding: Array,

    /* 对齐方向： start, end, auto */
    align: {
      type: String,
      default: "start",
      validator: (v) => ["start", "end", "auto"].includes(v),
    },
  },

  computed: {
    points() {
      const { start, end, padding, thickness, align } = this.$props;

      const [lsx = 0, lsy = thickness] = start;
      const [lex, ley] = end;
      const [sp, ep] = padding;

      const sx = { start: lsx, end: lex, auto: lsx }[align];
      const ex = { start: lsx, end: lex, auto: lex }[align];

      const [_1, _2, _3, _4] = [
        `${sx},${lsy - thickness / 2}`,
        `${sx + sp},${lsy - thickness / 2}`,
        `${ex + sp},${ley}`,
        `${ex + sp + ep},${ley}`,
      ];

      return `${_1} ${_2} ${_3} ${_4}`;
    },
  },
};
</script>