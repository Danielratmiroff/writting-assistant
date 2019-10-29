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
      <div class="textBox translate">
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

export default {
  name: 'translate',
    props: {
    msg: String,
    isTabActive: Boolean
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
                console.log(myJson);
                for (let key in myJson.matches) {
                  this.translationsText.push(myJson.matches[key].translation);  
                }
                console.log(this.translationsText)
                
            } catch (error) {
                console.error(error);
            }
        }
    }
}
  
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.container {
  width: 70%;
}

p {
  margin: 0 0.5rem 0 0;
}

.textboxes-wrap {
  display: flex;
  width: 100%;
  flex: 100%;
}

.inputLanguage {
  display: flex;
  justify-content: flex-start;
}

.translate {
  background-color: rgb(243, 243, 243)
}
</style>
