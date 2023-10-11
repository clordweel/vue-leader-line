<template>
  <vertical-leader-line
    v-bind="{ thickness, color }"
    :start="start"
    :end="end"
    :padding="padding_"
    style="position: absolute; top: 0; left: 0"
  />
</template>

<script>
import VerticalLeaderLine from "./VerticalLeaderLine";

export default {
  name: "LeaderLine",
  data() {
    return { start: [0, 0], end: [0, 0], padding_: [0, 0] };
  },
  props: {
    color: { type: String, default: "currentColor" },
    thickness: { type: Number, default: 2 },

    constraint: { type: Boolean, default: true },

    padding: {
      type: Array,
      default: () => [0, 0],
    },

    align: {
      type: String,
      default: "auto",
      validator: (v) => ["start", "end", "auto"].includes(v),
    },
  },
  components: {
    VerticalLeaderLine,
  },
  methods: {
    binds(startEl, endEl) {
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
        // offsetWidth: ew,
      } = endEl;

      let [sp, ep] = this.$props.padding;

      const align = this.$props.align;

      if (this.$props.constraint) {
        if (align === "auto") {
          sp = ep = (ex - sx) / 2 - sw / 2;
        } else if (align === "start") {
          ep = ex - sx - sw - sp;
        } else if (align === "end") {
          sp = ex - sx - sw - ep;
        }
      }

      this.$data.start = [sx + sw, sy + sh / 2];
      this.$data.end = [ex, ey + eh / 2];
      this.$data.padding_ = [sp, ep];
    },
  },
};
</script>
