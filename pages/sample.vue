<template>
  <div class="container">
    <button id="button" ref="button" @click="toggleTooltip">My Buttonn</button>
    <div id="tooltip" ref="tooltip" role="tooltip">
      そんな事より１よ、ちょいと聞いてくれよ。スレとあんま関係ないけどさ。
      このあいだ、近所の吉野家行ったんです。吉野家。
      そしたらなんか人がめちゃくちゃいっぱいで座れないんです。
      で、よく見たらなんか垂れ幕下がってて、１５０円引き、とか書いてあるんです。
      もうね、アホかと。馬鹿かと。
      <div id="arrow" ref="arrow" data-popper-arrow></div>
    </div>
  </div>
</template>

<script lang="ts">
import { Instance, createPopper } from "@popperjs/core";

type DataType = {
  show: boolean;
  popperInstance: null | Instance;
};

export default {
  data(): DataType {
    return {
      show: false,
      popperInstance: null,
    };
  },
  methods: {
    toggleTooltip() {
      console.log("start: toggleTooltip...");
      if (this.tooltip.hasAttribute("data-show")) {
        this.tooltip.removeAttribute("data-show");
      } else {
        this.tooltip.setAttribute("data-show", "");
        this.popperInstance?.update();
      }
    },
  },
  setup() {
    const button = ref();
    const tooltip = ref();

    return {
      button,
      tooltip,
    };
  },
  mounted() {
    this.button;
    this.popperInstance = createPopper(this.button, this.tooltip, {
      placement: "bottom-end",
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

<style lang="scss">
body {
  margin: 0;
  width: 1080px;
  overflow: scroll;
}

.container {
  background-color: #aaa;
  padding: 250px;

  #button {
    width: 400px;
    height: 400px;
    border-radius: 10px;
  }

  #tooltip {
    display: none;
    background: #fff;
    color: #643045;
    font-weight: bold;
    padding: 10px;
    font-size: 13px;
    border-radius: 4px;

    max-width: 300px;
  }
  #tooltip[data-show] {
    display: block;
  }
}

#arrow,
#arrow::before {
  position: absolute;
  width: 8px;
  height: 8px;
  background: inherit;
}

#arrow {
  visibility: hidden;
}

#arrow::before {
  visibility: visible;
  content: "";
  transform: rotate(45deg);
}

#tooltip[data-popper-placement^="top"] > #arrow {
  bottom: -4px;
}

#tooltip[data-popper-placement^="bottom"] > #arrow {
  top: -4px;
}

#tooltip[data-popper-placement^="left"] > #arrow {
  right: -4px;
}

#tooltip[data-popper-placement^="right"] > #arrow {
  left: -4px;
}
</style>
