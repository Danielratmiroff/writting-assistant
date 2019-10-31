<template>
  <div class="container">
    <div class="textboxes-wrap">
      <div>
        <div class="inputLanguage">
          <p>From</p>
          <select v-model="fromLanguage">
          <option disabled value="">any language</option>
          <option>en</option>
          <option>es</option>
          <option>de</option>
          <option>fr</option>
          <option>pr</option>
        </select>
        </div>
      <textarea
          class="textBox" 
          placeholder="Type here" 
          v-model="translateText"
          />
      </div>
      <div>
        <div class="inputLanguage"> 
            <p>To</p>
            <select v-model="toLanguage">
            <option disabled value="">any language</option>
            <option>en</option>
            <option>es</option>
            <option>de</option>
            <option>fr</option>
            <option>pr</option>
          </select>   
        </div>
      <div class="textBox results">
        <p
          v-for="(item, index) in translationsText"
          :key="item"
          >
          {{index}}
          {{item}}
        </p>
      </div>
      </div>
    </div>
    <button v-on:click="translate">
      Translate
    </button>
  </div>
</template>

<script>
import copyclipboard from './copyclipboard.vue'

export default {
  name: 'translate',
    props: {
    msg: String,
    isTabActive: Boolean
  },
  components: {
    copyclipboard
  },
  data() {
    return {  
        translateText : '',
        translationsText : [],
        fromLanguage : '',
        toLanguage : ''
      }
  },
  methods: { 
    async translate() {
            try {
                const response = await fetch('https://api.mymemory.translated.net/get?q=' + this.translateText + '!&langpair=' + this.fromLanguage + '|' + this.toLanguage);
                const myJson = await response.json();
                this.translationsText = [];
                for (let key in myJson.matches) {
                  this.translationsText.push(myJson.matches[key].translation);  
                }
            } catch (error) {
                console.error(error);
            }
        }
    }
}
  
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
.container {
  width: 70%;
}

.textboxes-wrap {
  display: flex;
  width: 100%;
  flex: 100%;
}

.textboxes-wrap > div {
  width: 50%
}

.inputLanguage {
  display: flex;
  justify-content: flex-start;
}

.results {
  background-color: rgb(243, 243, 243)
}
</style>
