<template>
  <div v-on:click="copy">
      <div
      :class="this.feedback ? 'feedback-popup' : 'feedback-hide'"
      >
        {{ this.feedback }}
      </div>
      <img alt="Copy" src="../assets/copy.svg" class="options-icon" />
    </div>
</template>

<script>

export default {
  name: 'copyclipboard',
  
  props: {
    msg: {
      type : String,
      required : true
    } 
  },

  data() {
    return {
      feedback : null
    }
  },

  methods: { 
    copy() {
        if (!this.msg) {
          this.feedback = 'Nothing to copy';
          setTimeout(this.deleteSuccessMsg, 2000)
          return
        }     
        let elem = document.querySelector('.textBox')
        try {
            elem.select();
            document.execCommand("copy");
            elem.selectionStart = elem.selectionEnd
            var successful = document.execCommand('copy');
            var msg = successful ? 'Successful' : 'Unsuccessful';
            this.feedback = `Copy ${msg}`;
            setTimeout(this.deleteSuccessMsg, 2000)

            } catch (err) {
                console.log('Oops, unable to copy');
            }        
       },
        deleteSuccessMsg() {
          this.feedback = null;
      }
    }
}
  
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.feedback-popup {
  display: block;
  position:absolute;
    left: 60%;
    bottom: 1rem;

}
.feedback-hide {
  display: none
}
</style>
