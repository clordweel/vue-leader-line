<template>
  <svg
    xmlns="http://www.w3.org/2000/svg"
    version="1.1"
    style="
      overflow: visible;
      height: 0.1px;
      width: 0.1px;
      top: 0;
      left: 0;
      z-index: 9999;
      position: absolute;
    "
  >
    <vertical-leader-line
      v-for="(line, i) in lines"
      :key="i"
      v-bind="{ thickness, color }"
      :start="line.start"
      :end="line.end"
      :padding="line.padding"
    />
  </svg>
</template>

<script>
import VerticalLeaderLine from "./VerticalLeaderLine";

export default {
  name: "LeaderLine",
  data() {
    return { lines: [], start: [0, 0], end: [0, 0], padding_: [0, 0] };
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
      default: "center",
      validator: (v) => ["start", "end", "center"].includes(v),
    },
  },
  components: {
    VerticalLeaderLine,
  },
  methods: {
    _calc(startEl, endEl) {
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

      return {
        start: [sx + sw, sy + sh / 2],
        end: [ex, ey + eh / 2],
        padding: [sp, ep],
      };
    },
    binds(startRef, endRef) {
      let endElements = [];

      if (!Array.isArray(endRef)) {
        endElements = [endRef];
      } else {
        endElements = endRef;
      }

      this.$data.lines = endElements.map((end) => this._calc(startRef, end));
    },
  },
};
</script>
