<script setup lang="ts">
import type { ShortLink } from '../models/ShortLink';

import BasePage from './BasePage.vue';
import Button from './Button.vue';
import InputField from './InputField.vue';
import { ref } from 'vue';
import ExclamationIcon from '../assets/exclamation.svg';

interface MainPageProps {
    links: readonly ShortLink[];
    hasError: boolean;
}

const inputText = ref('');

const props = defineProps<MainPageProps>();

const emit = defineEmits<{
    shortenLink: [text: string],
    removeLink: [text: string]
}>();
</script>

<template>
<BasePage :links="props.links" @removeLink="shortLink => $emit('removeLink', shortLink)">
    <div class="main-page-form-wrapper">
        <div class="main-page-form">
            <h2 class="heading-2 main-page-form__heading">Вставьте ссылку для сокращения</h2>
            <div class="main-page-form-elements">
                <InputField class="main-page__input-field" 
                    :text="inputText" 
                    @change="(value) => inputText = value" 
                    @keyup.enter="() => $emit('shortenLink', inputText)"
                />
                <Button label="Сократить" @click="() => $emit('shortenLink', inputText)" />
            </div>
            <div class="main-page__message" v-if="props.hasError">
                <ExclamationIcon class="message__exclamation-icon"/>
                <p class="message">Введенный текст не является ссылкой</p>
            </div>
        </div>
    </div>
</BasePage>
</template>

<style>
.main-page-form-wrapper {
    display: flex;
    justify-content: space-around;
    padding: 0px 24px;
}

.main-page-form {
    max-width: 520px;
    flex-grow: 1;
    display: flex;
    flex-direction: column;
    align-items: stretch;
}

.main-page-form-elements {
    display: flex;
    margin-top: 36px;
    justify-content: space-between;

}

.main-page__input-field {
    flex-grow: 1;
    margin-right: 12px;
}

.main-page-form__heading {
    text-align: center;
}

.message {
    color: white;
    font-family: Inter;
    font-size: 13px;
    line-height: 16px;
    padding: 8px 10px;

}

.main-page__message {
    background-color: #DA0000;
    max-width: 308px;
    max-height: 32px;
    display: flex;
    border-radius: 8px;
    margin-left: 36px;
    margin-top: 10px;
}

.message__exclamation-icon {
    display: flex;
    outline: none;
    border: none;
    background: none;
    margin-top: 6px;
    margin-left: 8px;
    width: 20px;
    height: 20px;
}
</style>
