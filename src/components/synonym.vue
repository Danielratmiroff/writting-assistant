<template>
    <div class="container">
      <p>Find Synonyms (English)</p>
    <div class="textboxes-wrap">
      <div>
          <textarea
          class="textBox" 
          placeholder="Type here" 
          v-model="getText"
          />
      </div>
    
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
    <button v-on:click="getSynonym">
      <p>Get Synonym</p>
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
p {
  text-align: left
}
</style>
