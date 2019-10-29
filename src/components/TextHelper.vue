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
    <textarea
        v-model="text.content" 
        id="textBox" 
        class="textBox" 
        placeholder="Type here" />

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
    </div>

    <p class="counters" v-if="isWordsActive">Words: {{ text.words }}</p>
    <p class="counters" v-if="isLengthActive">Characters: {{ text.len }}</p>
       
  </div>
</template>

<script>
export default {
  name: 'TextHelper',
  props: {
    msg: String
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
* {
  font-family: 'Courier New', Courier, monospace
}
.container {
   width: 70%;
   position: relative;
}
.menubar {
  width: 100%;
  display: flex;
  justify-content: space-between;
}
.settings {
  display: flex
}
.options {
  display: flex
}
.options-icon {
  width: 100%;
  max-width: 28px;
}
.textBox {
  width: 100%;
  height: 400px;
  position: relative;
  border: 2px solid #cdcdcd;
  border-color: rgba(0, 0, 0, .14);
  background-color: white;
  font-size: 14px;
  padding: 0.5rem;
}
.check, button {
    cursor: pointer;
    padding: 0.3rem 0.4rem;
    border: 1px solid #eeeeee;
    border-radius: 3px;
    border-bottom: none;
    display: flex;
    align-items: center;
}
.on {
    background-color: #4880f0;
    color:white
}
.counters{
  text-align: right;
  margin: 0.2rem 0.2rem 0 0;
  width: 100%;
  color: grey;
  font-size: 14px;
}
</style>
