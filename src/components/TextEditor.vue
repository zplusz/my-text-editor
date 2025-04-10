<template>
    <div class="editor-container">
      <div class="editor">
        <div class="toolbar">
          <!-- Text Formatting Buttons -->
          <button @click="applyBold">B</button>
          <button @click="applyItalic">I</button>
          <button @click="applyUnderline">U</button>
          <button @click="applyStrikethrough">S</button>
          
          <!-- Font Size & Color -->
          <select @change="applyFontSize" v-model="fontSize">
            <option value="1">Small</option>
            <option value="3">Medium</option>
            <option value="5">Large</option>
          </select>
          <input type="color" v-model="fontColor" @input="applyFontColor" />
          
          <!-- Text Alignment -->
          <button @click="applyAlignLeft">Left</button>
          <button @click="applyAlignCenter">Center</button>
          <button @click="applyAlignRight">Right</button>
          
          <!-- Background & Border -->
          <input type="color" v-model="bgColor" @input="applyBackgroundColor" />
          <button @click="applyBorder">Border</button>
          
          <!-- Insert Image and Link -->
          <button @click="insertImage">Insert Image</button>
          <button @click="insertLink">Insert Link</button>
        </div>
        <div
          class="editor-area"
          contenteditable="true"
          ref="editor"
          @input="onInputChange"
          :style="{ border: borderStyle, backgroundColor: bgColor }"
        ></div>
      </div>
      <div class="html-display">
        <h3>HTML Output</h3>
        <pre>{{ htmlContent }}</pre>
      </div>
    </div>
  </template>
  
  <script>
  import { ref } from 'vue';
  
  export default {
    setup() {
      const editor = ref(null);
      const htmlContent = ref('');
      const fontSize = ref('3');
      const fontColor = ref('#ffffff');
      const bgColor = ref('#000000');
      const borderStyle = ref('none');
      
      const onInputChange = () => {
        htmlContent.value = editor.value.innerHTML;
      };
  
      const applyBold = () => {
        document.execCommand('bold');
      };
  
      const applyItalic = () => {
        document.execCommand('italic');
      };
  
      const applyUnderline = () => {
        document.execCommand('underline');
      };
  
      const applyStrikethrough = () => {
        document.execCommand('strikeThrough');
      };
  
      const applyFontSize = () => {
        document.execCommand('fontSize', false, fontSize.value);
      };
  
      const applyFontColor = () => {
        document.execCommand('foreColor', false, fontColor.value);
      };
  
      const applyAlignLeft = () => {
        document.execCommand('justifyLeft');
      };
  
      const applyAlignCenter = () => {
        document.execCommand('justifyCenter');
      };
  
      const applyAlignRight = () => {
        document.execCommand('justifyRight');
      };
  
      const applyBackgroundColor = () => {
        document.execCommand('backColor', false, bgColor.value);
      };
  
      const applyBorder = () => {
        borderStyle.value = borderStyle.value === 'none' ? '1px solid #ccc' : 'none';
      };
  
      const insertImage = () => {
        const url = prompt('Enter image URL:');
        if (url) {
          document.execCommand('insertImage', false, url);
        }
      };
  
      const insertLink = () => {
        const url = prompt('Enter link URL:');
        if (url) {
          document.execCommand('createLink', false, url);
        }
      };
  
      return {
        editor,
        htmlContent,
        fontSize,
        fontColor,
        bgColor,
        borderStyle,
        onInputChange,
        applyBold,
        applyItalic,
        applyUnderline,
        applyStrikethrough,
        applyFontSize,
        applyFontColor,
        applyAlignLeft,
        applyAlignCenter,
        applyAlignRight,
        applyBackgroundColor,
        applyBorder,
        insertImage,
        insertLink,
      };
    },
  };
  </script>
  
  <style scoped>
  .editor-container {
    display: flex;
    justify-content: space-between;
    gap: 20px;
  }
  
  .editor {
    width: 50%;
    border: 1px solid #ccc;
    padding: 10px;
  }
  
  .toolbar {
    display: flex;
    flex-wrap: wrap;
    gap: 10px;
    margin-bottom: 10px;
  }
  
  .editor-area {
    min-height: 300px;
    border: 1px solid #ddd;
    padding: 10px;
  }
  
  button {
    padding: 5px 10px;
    cursor: pointer;
  }
  
  button:active {
    background-color: #f0f0f0;
  }
  
  input[type="color"] {
    width: 40px;
  }
  
  select {
    padding: 5px;
  }
  
  .html-display {
    width: 50%;
    border: 1px solid #ccc;
    padding: 10px;
    background-color: black;
    white-space: pre-wrap;
    word-wrap: break-word;
  }
  
  pre {
    font-family: monospace;
    margin: 0;
  }
  </style>
  