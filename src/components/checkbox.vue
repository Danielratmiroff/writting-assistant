<template>
  <div>
    <div
      v-on:click="LengthActive"
      class="check"
      v-bind:class="{ on: isLengthActive }"
    >
      <p>Characters</p>
      <div v-if="isLengthActive">
        <div class="stem" />
        <div class="kick" />
      </div>
    </div>
    <div
      v-on:click="WordsActive"
      class="check"
      v-bind:class="{ on: isWordsActive }"
    >
      <p>Characters</p>
      <div v-if="isWordsActive">
        <div class="stem" />
        <div class="kick" />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "checkbox",
  props: {},
  data() {
    return {
      checkObj: {},
      text: {
        content: "",
        len: 0,
        words: 0,
      },
      isLengthActive: false,
      isWordsActive: true,
    };
  },
  methods: {
    toggleActive() {
      // console.log(this.props)
    },
    LengthActive() {
      this.isLengthActive = !this.isLengthActive;
    },
    WordsActive() {
      this.isWordsActive = !this.isWordsActive;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.check {
  background: #ccc;
  width: 18px;
  height: 18px;
  margin-right: 5px;
  position: relative;
}
.on {
  background: #236bfa;
}
.stem {
  position: absolute;
  width: 3px;
  height: 9px;
  background-color: #fff;
  left: 8px;
  top: 5px;
  transform: rotate(45deg);
}
.kick {
  transform: rotate(45deg);
  position: absolute;
  width: 5px;
  height: 3px;
  background-color: #fff;
  left: 4px;
  top: 9px;
}
</style>
