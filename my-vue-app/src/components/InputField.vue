<template>
<input class="input-field" 
    type="text" 
    :value="props.text"
    @input="event => $emit('change', (event.target as HTMLInputElement).value)"
>
</template>


<script setup lang="ts">
interface InputFieldProps {
    text: string;
}

const props = defineProps<InputFieldProps>()
const emit = defineEmits<{
(e: 'change', value: string): void
}>()
</script>

<style>
.input-field {
    border-radius: 16px;
    padding: 15px 16px;
    outline: none;
    border: 0;

    font-family: Inter;
    font-size: 14px;
    line-height: 18px;
}
</style>