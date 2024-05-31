<script setup lang="ts">
import type { ShortLink } from '../models/ShortLink';

import BasePage from './BasePage.vue';
import Button from './Button.vue';
import InputField from './InputField.vue';
import { ref } from 'vue';

interface MainPageProps {
    links: readonly ShortLink[];
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
</style>
