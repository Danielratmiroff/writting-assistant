<template>
    <div class="container">
      <p class="subheading">
        Find Synonyms
        <span style="color:cornflowerblue;"> 
          (English only)
          </span>
          </p>
    <div class="textboxes-wrap">
        <div class="textWrap">
          <textarea
          class="textBox" 
          placeholder="Type here" 
          v-model="getText"
          />
      </div>
    <div class="textWrap">
        <div class="textBox results">
        <p
          v-for="(item, index) in synonymText"
          :key="item"
          >
          {{index}}
          {{item}}
        </p>
      </div>
    </div>
    </div>
    <button 
      class="triggerActionButton" 
      v-on:click="getSynonym"
      >
      Fetch Synonym
    </button>

  </div>
</template>

<script>

import copyclipboard from './copyclipboard.vue'

export default {
  name: 'synonym',
    props: {
    msg: String
  },
  components: {
    copyclipboard
  },
  data() {
    return {   
      getText : '',
      synonymText : [],  
      }
  },
  methods: { 
    async getSynonym() {
            try {
                const response = await fetch('https://words.bighugelabs.com/api/2/9f62706e1d0c54289deb02042ffec422/' + this.getText + '/json');
                const myJson = await response.json();
                this.synonymText = myJson.noun.syn;
            } catch (error) {
                console.error(error);
            }
        }
    }
}
  
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.subheading {
  text-align: left;
  margin-bottom: 0.4rem;
}
</style>
