<template>

  <div class="container">
    <div class="textWrap">
      <textarea
          v-model="text.content" 
          class="textBox" 
          placeholder="Type here" />
      <div class="options-secondary">
        <copyclipboard 
        class="copyclipboard" 
        :msg="this.text.content"
         /> 
      </div>
    </div>
    <div class="menubar"> 
      <div class="settings">
        <div v-on:click="WordsActive" 
          class='check'
          v-bind:class="{ on : isWordsActive }"> 
          Words
        </div>
          <div v-on:click="LengthActive" 
          class='check'
          v-bind:class="{ on : isLengthActive }"> 
          Chars
        </div>
      </div>
      <div class="counter-displays">
        <p class="counters" v-if="isWordsActive">
          Words: {{ text.words }}
          </p>
        <p class="counters" v-if="isLengthActive">
          Chars: {{ text.len }}
          </p>
      </div>
    </div>

  </div>
</template>

<script>
import copyclipboard from './copyclipboard.vue'

export default {
  name: 'TextHelper',
  props: {
    storage: Object
  },
  components: {
    copyclipboard
  },
  data() {
    return {
      text: {
        content : this.storage.text,
        len : this.storage.length,
        words: this.storage.word,
      },
      isLengthActive : false,
      isWordsActive : true
    }
  },
  watch: {
    'text.content' : function (content) {
      this.$emit('change-content', this.text);
      this.text.len = content.length;
      this.text.words = content.split(' ') ? 
                        content.length === 0 ? 0 :
                        content.split(' ').length : 0;
    }
  },
  methods: { 
    LengthActive() {
      this.isLengthActive = !this.isLengthActive
    },
    WordsActive() {
      this.isWordsActive = !this.isWordsActive
    } 
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.textBox {
  background-color: white;
}

.options-secondary {
  display: flex;
  justify-content: flex-end;
  width: 100%;
  margin: 0 -0.5rem 0.5rem;
}

.menubar {
  width: 100%;
  display: flex;
  justify-content: space-between;
  margin-top: 0.5rem
}

.settings {
  display: flex
}

.check {
    cursor: pointer;
    padding: 0.3rem 0.6rem;
    border: 1px solid #dddddd;
    display: flex;
    align-items: center;
}
.check:first-child {
    margin-right:0.2rem;
}

.on {
    background-color: #71a9fd;
    color:white
}


.counters{
  text-align: right;
  margin-left: 0.2rem;
  width: 100%;
  color: grey;
  font-size: 14px;
  white-space: nowrap;
}

.counters:first-child {
  margin-right: 1rem;
}

.counter-displays {
  display: flex;
  align-items: center;
}
</style>
