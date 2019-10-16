<template>
  <div class="input-wrapper">
    <div class="input-wrapper__leftpart leftpart">
      <img src="../assets/hugh.png" class="leftpart__img">
      <div v-if="onFocus" class="leftpart__round"></div>
    </div>
    <div class="input-wrapper__rightpart rightpart">
      <div :class="['rightpart__header', {'rightpart__header--blue': onFocus}]">Hugh is</div>
      <input
        class="input"
        v-model="year"
        @change.prevent="inputHandler"
        @focus="getBlueHeader"
        @blur="stopBlueHeader"
        ref="input"
        v-bind:style="getStyles"
      > hours old
    </div>
  </div>
</template>

<script>
export default {
  name: "inputGroup",
  data() {
    return {
      year: "",
      onFocus: false
    };
  },
  computed: {
    getStyles() {
      return {
        width:
          !this.year || this.year.length < 5
            ? "50px"
            : `${30 + this.year.length * 5}px`
      };
    }
  },
  methods: {
    inputHandler(e) {
      console.log(e)
      if (e.key === "Backspace") {
        const { year } = this;
        this.year = year.slice(0, -1);
        return;
      }

      this.getCaretPosition();
      const formatedYear = this.validateYear(e.value);
      this.year = this.splitByThree(formatedYear);
    },
    validateYear(inputVal) {
      return (this.year + inputVal).replace(/[^+\d]/g, "");
    },
    splitByThree(str) {
      return str.replace(/(\d)(?=(\d\d\d)+([^\d]|$))/g, "$1 ");
    },
    getBlueHeader() {
      this.onFocus = true;
    },
    stopBlueHeader() {
      this.onFocus = false;
    },
    getCaretPosition() {
      const { input } = this.$refs;
      input.addEventListener("keydown", function() {
        console.log("Caret position: " + this.selectionStart);
      });
    }
  }
};
</script>

<style lang="scss" scoped>
.input-wrapper {
  display: flex;
  flex-flow: row nowrap;
  font-size: 13px;
}
.rightpart {
  margin-left: 16px;
  &__header {
    font-weight: 700;
    font-size: 13px;
    text-transform: uppercase;
    &--blue {
      color: #2540ff;
    }
  }
}
.leftpart {
  position: relative;
  &__round {
    position: absolute;
    width: 56px;
    top: -1px;
    right: -1px;
    height: 56px;
    border-radius: 50%;
    border: 2px #2540ff solid;
  }
  &__img {
    width: 55px;
    height: 55px;
  }
}
.input {
  border: none;
  padding: 10px 0;
  outline: none;
  border-bottom: 1px #c9c9cf solid;
  color: #c9c9cf;
  font-weight: 700;
  &:focus {
    border-bottom: 1px #2540ff solid;
    color: black;
  }
}
</style>
