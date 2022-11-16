<template>
<div class="editor-container">
	<button class="done-btn" @click="userDone">Done</button>
	<textarea
		class="text-input"
		ref="input"
		autofocus
	></textarea>
</div>
</template>

<script setup lang="ts">
import {ref, defineEmits, defineProps, onMounted} from 'vue' 
const input = ref<HTMLTextAreaElement | null>(null)
const emit = defineEmits(['done'])
const props = defineProps(['initial'])

const userDone = () => {
	if (!input.value) return
	emit('done', input.value.value)
}

onMounted(() => {
	if (!input.value) return
	input.value.value = props.initial
})
</script>

<style scoped>
.editor-container {
height: 100%;
overflow: hidden;
box-sizing: border-box;
display: flex;
flex-direction: column;
width: 48ch;
max-width: 100%;
cursor: pointer;
}
.done-btn {
width: 100%;
border: none;
padding: 0.5rem;
background: rgba(255,255,255,0.05);
border-bottom: 4px solid rgba(0,0,0,0.35);
box-sizing: border-box;
display: block;
color: rgba(255,255,255,0.5);
transition: background 300ms ease-in-out;
}
.done-btn:active {
background: rgba(255,255,255,0.09);
}
.text-input {
border: none;
background: rgba(0,0,0,0.1);
resize: none;
width: 100%;
font-size: 1.1rem;
padding: 0.5rem;
line-height: 1.5;
flex: 1;
}
.text-input:focus {
outline: none;
}
</style>