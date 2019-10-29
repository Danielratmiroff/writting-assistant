<template>
  <div>
    <button v-on:click="copy">
      <img alt="Copy" src="../assets/copy.svg" class="options-icon" />
    </button>
  </div>
</template>

<script>

export default {
  name: 'copyclipboard',
    props: {
    msg: String
  },
  methods: { 
    copy() {
        if (!this.msg) {
            console.log('Nothign to copy');
            return
        }     
        let elem = document.getElementById('textBox')
        try {
            elem.select();
            document.execCommand("copy");
            elem.selectionStart = elem.selectionEnd
            var successful = document.execCommand('copy');
            var msg = successful ? 'successful' : 'unsuccessful';
            console.log('Copying text command was ' + msg);
            } catch (err) {
                console.log('Oops, unable to copy');
            }
       },
    }
}
  
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
