<template>
 <!-- 
   separate different components -- DONE
   Create translate display -- DONE 
   Create synonym display  -- DONE
   Adjust Copyclipboard to work in all areas
   Design TextHelper layout
   Design Translate layout
   Design Synonym layout
   Design Options Tabs layout 
   Convert checkbox into component  
   Refactor CSS 
   Create Footer
 -->

  <div class="container">
    <div class="textWrap">
      <textarea
          v-model="text.content" 
          class="textBox" 
          placeholder="Type here" />
      <div class="options-secondary">
        <copyclipboard class="copyclipboard" /> 
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
        <p class="counters" v-if="isWordsActive">Wrds: {{ text.words }}</p>
        <p class="counters" v-if="isLengthActive">Chrs: {{ text.len }}</p>
      </div>
    </div>

  </div>
</template>

<script>
import copyclipboard from './copyclipboard.vue'

export default {
  name: 'TextHelper',
  props: {
    msg: String
  },
  components: {
    copyclipboard
  },
  data() {
    return {
      text: {
        content : '',
        len : 0,
        words: 0,
      },
      isLengthActive : false,
      isWordsActive : true
    }
  },
  watch: {
    'text.content' : function (content) {
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

.textWrap {
  background-color: white;
  height: 400px;
  font-size: 14px;
  padding: 0.5rem;
  display: flex;
  flex-direction: column;
  position: relative;
}

.textBox {
  background-color: white;
  border: none;
  resize: none;
  width: 100%;
  flex-grow: 1;
}

.options-secondary {
  display: flex;
  justify-content: flex-end;
  width: 100%;
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
    padding: 0.3rem 0.4rem;
    border: 1px solid #dddddd;
    display: flex;
    align-items: center;
    margin: 0 0.2rem;
}

.on {
    background-color: #4880f0;
    color:white
}


.counters{
  text-align: right;
  margin-left: 0.2rem;
  width: 100%;
  color: grey;
  font-size: 14px;
}

.counter-displays {
  display: flex;
  align-items: center;
  
}
</style>
