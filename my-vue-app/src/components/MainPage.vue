<template>
<p>LinkShortener111</p>
<h2>Вставьте ссылку для сокращения</h2>
<InputField :text="inputLink" @change="(value) => inputLink = value"/>
<Button label="Сократить" @click = "() => console.log(inputLink)"/>
</template>

<script setup lang="ts">
import Button from './Button.vue'
import InputField from './InputField.vue';
import {ref} from 'vue'
const inputLink = ref('')
</script>

<style>
</style>
