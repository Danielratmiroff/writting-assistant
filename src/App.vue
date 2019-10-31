<template>
  <div id="app">
    <!-- <img alt="DR Logo" src="./assets/logo.png" class="main-logo"> -->
    <h1>
      My write.
    </h1>
    <h2>
      Make your writing easier.
    </h2>
     <div class="options">
      <div class="tabs">
        <button v-on:click="activeTab('textHelper')">
          <img alt="textHelper" src="./assets/write.png" class="options-icon" />
        </button>

        <button v-on:click="activeTab('translate')">
          <img alt="Translate" src="./assets/translate.jpg" class="options-icon" />
        </button>

        <button v-on:click="activeTab('synonym')">
          <img alt="Synonym" src="./assets/synonym.png" class="options-icon" />
        </button>
      </div>       
    </div>

    <TextHelper v-if="isActive ==='textHelper'"/> 
    <translate v-else-if="isActive ==='translate'"/>
    <synonym v-else />
    
    <footer class="footer">
          here is my
    </footer>
  </div>
</template>

<script>
import TextHelper from './components/TextHelper.vue'
import translate from './components/translate.vue'
import synonym from './components/synonym.vue'
import checkbox from './components/checkbox.vue'

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
       isActive : "textHelper"
     }
  },
  methods: {
    activeTab(tab) {
      this.isActive = tab;
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
  font-family: 'Courier New', Courier, monospace
}

p {
  margin: 0 0.5rem 0 0;
}

input:focus,
select:focus,
textarea:focus,
button:focus {
    outline: none;
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  display: flex; 
  align-items: center;
  flex-direction: column;
}

.options, .tabs {
  display: flex;
}

.options {
  width: 70%;
  margin-bottom: 1rem;
  justify-content: space-between;
  position: relative;
}

.options-icon {
  width: 100%;
  max-width: 28px;
}

.container {
   width: 70%;
   position: relative;
}


.check, button {
    cursor: pointer;
    padding: 0.3rem 0.4rem;
    border-radius: 3px;
    display: flex;
    align-items: center;
    border: 1px solid grey;
}

.textBox {
  background-color: white;
  border: none;
  resize: none;
  width: 100%;
  flex-grow: 1;
}


footer { 
  position: absolute;
  bottom: 0px;
}

.main-logo {
  width: 20%;
  height: auto;
  margin: 5rem 0 2rem 0;
}
</style>
