<script setup lang="ts">
import type { ShortLink } from '../models/ShortLink';

import BasePage from './BasePage.vue';
import Button from './Button.vue';
import CopyIcon from '../assets/copy.svg';
// import { ref } from 'vue';

interface LinkCreatedPageProps {
    createdLink: ShortLink;
    links: readonly ShortLink[];
}

const props = defineProps<LinkCreatedPageProps>();

const emit = defineEmits<{
    shortenAnotherLink: [],
    removeLink: [text: string]
}>();

function copyToClipboard() {
    navigator.clipboard.writeText(props.createdLink.shortUrl);
}
</script>

<template>
<BasePage :links="props.links" @removeLink="shortLink => $emit('removeLink', shortLink)">
    <div class="shortlink-card-wrapper">
        <div class="shortlink-card">
            <div class="shortlink-container">
                <div class="shortlink-container__url-wrapper">
                    <a class="shortlink-container__url" :href="props.createdLink.shortUrl">
                        {{ props.createdLink.shortUrl }}
                    </a>
                    <button class="url-wrapper__copy-button" @click="copyToClipboard">
                        <CopyIcon class="url-wrapper__copy-icon" />
                    </button>
                </div>
            </div>
            <div class="shortlink-card-info">
                <div class="shortlink-card-info-link">
                    <p class="shortlink-card-info-link__label">Ссылка</p>
                    <p class="shortlink-card-info-link__text">{{ props.createdLink.originalUrl }}</p>
                </div>
                <Button label="Сократить другую ссылку" @click="() => $emit('shortenAnotherLink')" />
            </div>
        </div>
    </div>
</BasePage>
</template>

<style>
.shortlink-card-wrapper {
    display: flex;
    justify-content: space-around;
}

.shortlink-card {
    max-width: 496px;
    flex-grow: 1;
    display: flex;
    flex-direction: column;
    background-color: #fff;
    border-radius: 20px;
}

.shortlink-container {
    display: flex;
    align-items: center;
    height: 120px;
    justify-content: space-around;
    border-bottom: 1px solid #E7EBF3;
}

.shortlink-container__url-wrapper {
    display: flex;
    align-items: center;
}

.shortlink-container__url {
    font-family: Inter;
    font-size: 18px;
    line-height: 24px;
    color: #2E2BCA;
    text-decoration: none;
}

.url-wrapper__copy-button {
    margin-left: 12px;
    padding: 0;
    outline: none;
    border: none;
    background: none;
    display: flex;
}

.url-wrapper__copy-button:hover {
    cursor: pointer;
}

.url-wrapper__copy-icon {
    margin: 0;
    padding: 0;
}

.shortlink-card-info {
    padding: 20px 24px 24px 24px;
    display: flex;
    flex-direction: column;
}

.shortlink-card-info-link {
    display: flex;
    flex-direction: column;
    margin-bottom: 32px;
}

.shortlink-card-info-link__label {
    margin-bottom: 10px;
}
</style>
