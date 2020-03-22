 <!-- 
   Make Responsive
   Make keyboard accessible
   Convert checkbox into component  
   Convert textarea into component
   Refactor CSS 
 -->

<template>
  <div id="app">
    <h1>
      Easy Write
    </h1>
    <h2>
      Make your writing simpler
    </h2>
     <div class="options">
      <div class="tabs">
        <button 
          v-on:click="activeTab('textHelper')"
          v-bind:class="this.isActive === 'textHelper' ? 'activeTabButton' : null"
          >
          <img alt="textHelper" src="./assets/write.png" class="options-icon" />
        </button>

        <button
         v-on:click="activeTab('translate')"
         v-bind:class="this.isActive === 'translate' ? 'activeTabButton' : null"
         >
          <img alt="Translate" src="./assets/translate.jpg" class="options-icon" />
        </button>

        <button 
          v-on:click="activeTab('synonym')"
          v-bind:class="this.isActive === 'synonym' ? 'activeTabButton' : null"
          >
          <img alt="Synonym" src="./assets/synonym.png" class="options-icon" />
        </button>
      </div>       
    </div>

    <TextHelper v-if="isActive ==='textHelper'" 
            v-on:change-content="saveContent"
            :storage='save'
            /> 
    <translate v-else-if="isActive ==='translate'"/>
    <synonym v-else />
    
    <footer class="footer">
             <img class="footer-logo" src="./assets/logo.png" />
          <p>
          DR © 2019
          </p>
          <a class="github-link"
            href="https://github.com/Danielratmiroff/writingassistant.github.io.git">
            Find this project in Github
          </a>
    </footer>
  </div>
</template>

<script>
import TextHelper from './components/TextHelper.vue'
import translate from './components/translate.vue'
import synonym from './components/synonym.vue'
import checkbox from './components/checkbox.vue'
// msg=this.saveText;
export default {
  name: 'app',
  components: {
    TextHelper,
    translate,
    synonym,
    checkbox
  },
  data() {
     return {
       isActive : "textHelper",
       save: { 
         text : '',
         length : 0,
         word : 0
       }
     }
  },
  methods: {
    activeTab(tab) {
      this.isActive = tab;
    },
    saveContent(value) {
        this.save.text = value.content;
        this.save.length = value.len;
        this.save.word = value.words;
    }
  }
}

</script>

<style>
html, body {
  margin: 0;
  height: 100%;
  background-color: aliceblue
}

* {
  font-family: 'Montserrat', sans-serif
}

p {
  margin: 0;
}

input:focus,
select:focus,
textarea:focus,
button:focus {
    outline: none;
}

#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  display: flex; 
  height: 100%;
  align-items: center;
  flex-direction: column;
  overflow: hidden;
  -ms-flex: 1 1 auto;
  flex: 1 1 auto;
}



.options, .tabs {
  display: flex;
}

.options {
  width: 70%;
  margin: 1.5rem 0;
  justify-content: space-between;
  position: relative;
}

.options-icon {
  width: 100%;
  max-width: 28px;
  display: flex;
}

.container {
   width: 70%;
   position: relative;
}

.check, button {
    cursor: pointer;
    border-radius: 3px;
}

check {
  padding: 0.3rem .5rem;
}

button {
  margin-right: 0.3rem;
  padding: 0.35rem 1rem;
  border: #dddddd 1px solid;
  background: none;
}

.activeTabButton {
  background-color: #dddddd;
}

.textWrap {
  background-color: white;
  height: 400px;
  font-size: 14px;
  display: flex;
  flex-direction: column;
  position: relative;
  overflow: hidden;
  padding: 0.3rem;
}

.textBox {
  border: none;
  resize: none;
  flex-grow: 1;
  text-align: left
}

.triggerActionButton {
  width: 100%;
  max-width: 250px;
  border: none;
  margin-top: 0.7rem;
  padding: 0.7rem 1rem;
  background-color: #236bfa;
  text-align: center;
  color: white;
  font-size: 16px;
}

footer { 
  width: 100%;
  padding: 1.5rem 0;
  background-color: rgb(0, 0, 0);
  line-height: 1.5;
  font-size: 0.8rem;
  margin-top: 4rem;
  color: white
}

.footer-logo {
  margin: 0 auto;
  width: 7%;
}

.github-link {
  color: white
}
</style>
