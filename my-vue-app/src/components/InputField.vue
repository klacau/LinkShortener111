<template>
<input class="in" type="text" 
:value="text"
@input= "event => $emit('change', event.target!.value)"
>
</template>


<script setup lang="ts">
import type {Ref} from 'vue'
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