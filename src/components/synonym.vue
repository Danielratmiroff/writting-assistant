<template>
    <div class="container">
    <div class="textboxes-wrap">
      <div>
          <textarea
          class="textBox" 
          placeholder="Type here" 
          v-model="getText"
          />
      </div>
    
        <div class="textBox synonyms">
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

export default {
  name: 'synonym',
    props: {
    msg: String
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

.synonyms {
  background-color: rgb(243, 243, 243)
}
</style>
