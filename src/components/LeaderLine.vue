<template>
  <vertical-leader-line
    :start="start"
    :end="end"
    :padding="padding_"
    align="start"
    v-bind="{ thickness, color }"
    style="position: absolute; top: 0; left: 0"
  />
</template>

<script>
import VerticalLeaderLine from "./VerticalLeaderLine";

export default {
  name: "VerticalLeaderLineZ",
  data() {
    return { start: [0, 0], end: [0, 0], padding_: [0, 0] };
  },
  props: {
    /* 线条颜色 */
    color: { type: String, default: "currentColor" },
    /* 线条粗细 */
    thickness: { type: Number, default: 2 },

    padding: {
      type: Array,
      default: () => [0, 0],
    },

    /* 对齐方向： start, end, auto */
    align: {
      type: String,
      default: "auto",
    },
  },
  components: {
    VerticalLeaderLine,
  },
  mounted() {},
  methods: {
    binds(startEl, endEl) {
      // console.log(startEl, endEl);

      const {
        offsetLeft: sx,
        offsetTop: sy,
        offsetHeight: sh,
        offsetWidth: sw,
      } = startEl;
      const {
        offsetLeft: ex,
        offsetTop: ey,
        offsetHeight: eh,
        offsetWidth: ew,
      } = endEl;

      // console.log(sx, sy, sw, sh);
      // console.log(ex, ey, ew, eh);
      this.$data.start = [sx + sw, sy + sh / 2];
      this.$data.end = [ex + ew, ey + eh / 2];

      const align = this.$props.align;

      let [sp, ep] = this.$props.padding;

      if (align === "auto") {
        sp = ep = (ex - sx) / 2 - sw / 2;
      } else if (align === "start") {
        ep = ex - sx - sw - sp;
      } else if (align === "end") {
        sp = ex - sx - sw - ep;
      }

      // console.log(align, sp, ep);

      this.$data.padding_ = [sp, ep];
    },
  },
};
</script>