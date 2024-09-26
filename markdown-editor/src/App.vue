<script>
import { debounce } from 'lodash-es';
import { marked } from 'marked';


export default {
  data: ()=>({
    input: `# hello`
  }),
  computed: {
    output(){
      return marked(this.input)
    }
  },
  methods: {
    update: debounce(function(e){
      this.input = e.target.value
    }, 100)
  },

}
</script>

<template>
<div class="editor">
  <textarea :value="input" @input="update" class="input">

  </textarea>
  <div class="output" v-html="output"></div>
</div>

</template>
<style>
.editor{
  height: 100vh;
  display: flex;
}
.input, .output{
  overflow: auto;
  width: 50%;
  height: 100%;
  padding: 0 20px;
  box-sizing: border-box;
}

.input {
    border: none;
    border-right: 1px solid #ccc;
    padding: 20px;
    font-size: 16px;
    background: #f6f6f6;
    outline: none;
    resize: none;
    font-family: 'Monaco', couriar, monospace;
}

code{
  color: #f66;
}
</style>