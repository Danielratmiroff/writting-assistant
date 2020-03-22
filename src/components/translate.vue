<template>
  <div class="container">
    <div class="textboxes-wrap">
      <div>
        <div class="inputLanguage">
          <p>Translate From</p>
          <select class="inputSelect" v-model="fromLanguage">
            <option disabled value>any language</option>
            <option value="en">English</option>
            <option value="es">Spanish</option>
            <option value="de">Deutsch</option>
            <option value="fr">French</option>
          </select>
        </div>
        <div class="textWrap">
          <textarea
            class="textBox"
            placeholder="Type here (English, Spanish, Deutsch, French)"
            v-model="translateText"
          />
        </div>
      </div>
      <div>
        <div class="inputLanguage">
          <p>Into</p>
          <select class="inputSelect" v-model="toLanguage">
            <option disabled value>any language</option>
            <option value="en">English</option>
            <option value="es">Spanish</option>
            <option value="de">Deutsch</option>
            <option value="fr">French</option>
          </select>
        </div>
        <div class="textWrap">
          <div class="textBox results">
            <p v-for="(item, index) in translationsText" :key="item">
              {{item}}
            </p>
          </div>
        </div>
      </div>
    </div>
    <button class="triggerActionButton" v-on:click="translate">Translate</button>
  </div>
</template>

<script>
import copyclipboard from "./copyclipboard.vue";

export default {
  name: "translate",
  props: {
    msg: String,
    isTabActive: Boolean
  },
  components: {
    copyclipboard
  },
  data() {
    return {
      translateText: "",
      translationsText: [],
      fromLanguage: "en",
      toLanguage: "es"
    };
  },
  methods: {
    async translate() {
      try {
        const response = await fetch(
          "https://api.mymemory.translated.net/get?q=" +
            this.translateText +
            "!&langpair=" +
            this.fromLanguage +
            "|" +
            this.toLanguage
        );
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
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style >
.container {
  width: 70%;
}

.textboxes-wrap {
  display: flex;
  width: 100%;
  flex: 100%;
}

.inputSelect {
  border: none;
  background: no-repeat;
  color: cornflowerblue;
  cursor: pointer;
  font-size: 0.9rem;
  font-weight: 600;
  margin-left: 0.5rem;
}

.textBox {
  background-color: white;
}

.textboxes-wrap > div {
  width: 50%;
  margin: 0 0.2rem;
}

.inputLanguage {
  display: flex;
  justify-content: flex-start;
  margin-bottom: 0.4rem;
}

.results {
  background-color: rgb(255, 255, 255);
}
</style>
