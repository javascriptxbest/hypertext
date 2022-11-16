<template>
  <div class="container">
    <div v-if="mode === modes.main">
      <button class="mode-button">Preview</button>
      <button class="mode-button" @click="setMode(modes.text)">Edit Text</button>
      <pre>
        {{data.text}}
      </pre>
    </div>
    <text-input 
      v-if="mode === modes.text" 
      :initial="data.text" 
      @done="handleTextEditDone" />
  </div>
</template>

<script setup lang="ts">
import {ref} from 'vue'
const modes = {main: 'main', text: 'text'}
type Mode = typeof modes[keyof typeof modes]
const mode = ref('main')
const data = {
  text: ''
}
const setMode = (newmode: Mode) => {
  mode.value = newmode
}
const handleTextEditDone = (newText: string) => {
  data.text = newText
  setMode(modes.main)
}
</script>

<style scoped>
.container {
  height: 100%;
}
.mode-button {
  display: block;
  width: 100%;
  border: none;
  background: rgba(255,255,255,0.1);
  padding: 0.5rem;
  border-bottom: 3px solid rgba(0,0,0,0.2);
  cursor: pointer;
}
</style>