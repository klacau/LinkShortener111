<template>
<input class="in" type="text" 
:value="props.text"
@input= "event => $emit('change', (event.target as HTMLInputElement).value)"
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
.in {
    border-radius: 16px;
    padding: 15px 16px;

}
</style>