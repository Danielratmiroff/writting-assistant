<template>
  <div v-on:click="copy">
      <div 
      :class="this.feedback ? 'feedback-popup' : null"
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
            console.log('Nothing to copy');
            return
        }     
        let elem = document.querySelector('.textBox')
        try {
            elem.select();
            document.execCommand("copy");
            elem.selectionStart = elem.selectionEnd
            var successful = document.execCommand('copy');
            var msg = successful ? 'successful' : 'unsuccessful';
            this.feedback = 'Copying text command was ' + msg;
            console.log(this.feedback);
            } catch (err) {
                console.log('Oops, unable to copy');
            }
       },
    }
}
  
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.feedback-popup {
  display: block
}
</style>
