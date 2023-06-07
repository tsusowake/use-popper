<template>
  <div class="tooltip-wrapper">
    <div ref="content" class="content" @click="toggleTooltip">
      <slot name="content"></slot>
    </div>
    <div ref="tooltip" class="tooltip" role="tooltip">
      <slot name="tooltip"></slot>
      <div class="tooltip-arrow" ref="arrow" data-popper-arrow></div>
    </div>
  </div>
</template>

<script lang="ts">
import { Instance, Placement, createPopper } from "@popperjs/core";

type DataType = {
  show: boolean;
  popperInstance: null | Instance;
};

type Props = {
  placement: Placement;
};

export default {
  props: {
    placement: {
      type: String,
      default: "top",
    },
  },
  data(): DataType {
    return {
      show: false,
      popperInstance: null,
    };
  },
  methods: {
    toggleTooltip() {
      if (this.tooltip.hasAttribute("data-show")) {
        this.tooltip.removeAttribute("data-show");
      } else {
        this.tooltip.setAttribute("data-show", "");
        this.popperInstance?.update();
      }
    },
  },
  setup() {
    const content = ref();
    const tooltip = ref();

    return {
      content,
      tooltip,
    };
  },
  mounted() {
    this.content;
    this.popperInstance = createPopper(this.content, this.tooltip, {
      placement: this.placement as Placement,
      modifiers: [
        {
          name: "offset",
          options: {
            offset: [0, 8],
          },
        },
      ],
    });
  },
};
</script>

<style lang="scss" scoped>
.tooltip {
  display: none;
  background: #fff;
  color: #643045;
  font-weight: bold;
  padding: 10px;
  font-size: 13px;
  border-radius: 4px;
  max-width: 300px;

  &[data-show] {
    display: block;
  }

  .tooltip-arrow,
  .tooltip-arrow::before {
    position: absolute;
    width: 8px;
    height: 8px;
    background: inherit;
  }

  .tooltip-arrow {
    visibility: hidden;
    &::before {
      visibility: visible;
      content: "";
      transform: rotate(45deg);
    }
  }

  &[data-popper-placement^="top"] > .tooltip-arrow {
    bottom: -4px;
  }

  &[data-popper-placement^="bottom"] > .tooltip-arrow {
    top: -4px;
  }

  &[data-popper-placement^="left"] > .tooltip-arrow {
    right: -4px;
  }

  &[data-popper-placement^="right"] > .tooltip-arrow {
    left: -4px;
  }
}
</style>
