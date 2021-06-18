<template>
  <div id="App">
    <div id="headingDiv">
      <button class="heading" @click="handleHeading(1)">H</button>
     <button class="addIn" @click="handleAddIn('**Big**')"><b>B</b></button>
<button class="addIn" @click="handleAddIn('*italic*')"><i>i</i></button>
<button class="addIn" @click="handleAddIn('~~strikethrough~~')"><del>s</del></button>
      <button class="addIn" @click="handleAddIn('-   ')">⚈</button>
      <button class="addIn" @click="handleAddIn('1. ')">📝</button>
      <button class="addIn" @click="handleAddIn('- [x] ')">✅</button>
      <button class="addIn" @click="handleAddIn('> *“To be, or not to be, that is the question - Hamlet”*')">💬</button>
      <button class="addIn" @click="handleAddIn('```<p>My first paragraph.</p>```')">👨‍💻</button>
      <button class="addIn" @click="handleAddIn('![alt text](url)')">🖼️</button>
      <button class="addIn" @click="handleAddIn('[alt text](url)')">🔗</button>
      <button class="addIn" @click="handleAddIn('---')">―</button>



    </div>
    <div id="editorDiv">
      <div id="editorWindow">
        <textarea id="editor" v-model="inputText"></textarea>
      </div>
      <div id="displayWindow">
        <div id="display" v-html="stylizedMarkdown"></div>
      </div>
    </div>
  </div>
</template>

<script>
import marked from "marked";
import DOMPurify from "dompurify";

export default {
  name: "App",
  components: {},
  data: () => {
    return {
      inputText: "# Welcome To Markdown Editor ✍️ ",
    };
  },
  computed: {
    stylizedMarkdown() {
      let output = DOMPurify.sanitize(marked(this.inputText));
      console.log(output);
      return output;
    },
  },
  methods: {
    handleHeading(size) {
      this.inputText = this.inputText + "#".repeat(size) + " ";
    },
    handleAddIn(type) {
      this.inputText = this.inputText + type;
    },
  },
};
</script>

<style lang="scss">

body {
    background-color: #ffffff;
  }

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;

  #editorDiv {
    display: flex;
  }

  #editorWindow,
  #displayWindow {
    padding-top: 20px;
    width: 40%;
  }

  #displayWindow {
    padding-left: 1rem;
  }

  #editorWindow {
    margin-right: 1rem;

    #editor {
              background-color: #f5f5f5;
      border: none;
      height: 100vh;
      width: 99%;
      resize: none;
      font-size: 1.25rem;
      border-radius: 10px;
color: #9c9c9c;
    }
  }

  #headingDiv {
    button {
      background-color: #f5f5f5;
      border: 1px solid;
      margin: 5px;
      border-radius: 20px;
    }
  }
}
</style>
