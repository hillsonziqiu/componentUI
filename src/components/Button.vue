<template>
  <div
    class="button"
    :class="[
      type === 'normal' ? 'button' : 'word-button',
      { disabled: disabled },
      size,
      type === 'normal' ? `bg-${color}` : color,
      type === 'normal' ? `angle-${angle}` : ''
    ]"
    @click="_click"
  >
    <slot
      class="button-icon button-pre"
      :class="`button-icon-${size}`"
      name="pre"
    ></slot>
    <p class="button-value">
      <slot></slot>
    </p>
    <!-- <div class="button-icon button-suff"> -->
    <slot
      name="suff"
      class="button-icon button-suff"
      :class="`button-icon-${size}`"
    ></slot>
    <!-- </div> -->
  </div>
</template>

<script>
// defined default dict
const SizeDict = ["mini", "small", "middle", "large"];
const ColorDict = ["primary", "green", "blue", "yellow", "red", "gray"];
const AngleDict = ["angle-right", "angle-fillet"];
const TypeDict = ["normal", "word"];

function validValue(val, valMap) {
  const valM = new Set(valMap);
  return valM.has(val);
}

export default {
  name: "Button",
  props: {
    color: {
      type: String,
      validate(val) {
        return validValue(val, ColorDict);
      },
      default: "primary"
    },
    size: {
      type: String,
      validate(val) {
        return validValue(val, SizeDict);
      },
      default: "small"
    },
    angle: {
      type: String,
      validate(val) {
        return validValue(val, AngleDict);
      },
      default: "fillet"
    },
    type: {
      type: String,
      validate(val) {
        return validValue(val, TypeDict);
      },
      default: "normal"
    },
    disabled: {
      type: Boolean,
      default: false
    }
  },
  data() {
    return {};
  },
  methods: {
    _click() {
      this.$emit("click");
    }
  }
};
</script>

<style lang="less" scoped>
@import url("./../assets/less/commonVar.less");
.button {
  display: inline-flex;
  flex-direction: row;
  justify-content: flex-start;
  align-items: center;
  user-select: none;
  cursor: pointer;
  .button-value {
    padding: 0 10px;
  }
  .button-icon-mini {
    width: @distanceMini;
    height: @distanceMini;
  }
  .button-icon-small {
    width: @distanceSmall;
    height: @distanceSmall;
  }
  .button-icon-middle {
    width: @distanceMiddle;
    height: @distanceMiddle;
  }
  .button-icon-large {
    width: @distanceLarge;
    height: @distanceLarge;
  }
}
.word-button {
  color: #009eff;
  user-select: none;
  cursor: pointer;
}
</style>
