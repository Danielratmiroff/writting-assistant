<template>
  <div id="app">
    <img alt="DR Logo" src="./assets/logo.png" class="main-logo">
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
      <copyclipboard v-bind:msg="hello" />        
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
import copyclipboard from './components/copyclipboard.vue'
import translate from './components/translate.vue'
import synonym from './components/synonym.vue'
import checkbox from './components/checkbox.vue'

export default {
  name: 'app',
  components: {
    TextHelper,
    copyclipboard,
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
  justify-content: space-between;
  width: 70%;
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
