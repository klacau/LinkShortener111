<script setup lang="ts">
interface ButtonProps {
    label: string;
}

const props = defineProps<ButtonProps>();
</script>

<template>
    <button class="btn" type="button">
        {{ props.label }}
    </button>
</template>

<style>
.btn {
    font-size: 14px;
    font-family: Inter;
    font-weight: 600;
    line-height: 18px;
    letter-spacing: 2%;
    background-color: #1A243F;
    color: #fff;
    padding: 15px 26px;
    border-radius: 16px;
    border: 0;
    outline: none;
}
.btn:hover {
    cursor: pointer;
    background-color: #01081b; 
}
</style>
