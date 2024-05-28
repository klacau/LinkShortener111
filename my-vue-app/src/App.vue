<script setup lang="ts">
import type { ShortLink } from './models/ShortLink';

import MainPage from './components/MainPage.vue';
import { ref, Ref } from 'vue';

const linksValue = localStorage.getItem('links');
const storageLinks: ShortLink[] = linksValue === null ? [] : JSON.parse(linksValue);

const links: Ref<ShortLink[]> = ref(storageLinks);

function shortenLink(text: string) {
    const shortenedUrl = `https://localhost:0000/kS9wQ${Math.round(Math.random() * 9)}`;
    
    const shortLink: ShortLink = {
        shortUrl: shortenedUrl,
        originalUrl: text,
        createdAt: new Date()
    };

    links.value.push(shortLink);
    localStorage.setItem('links', JSON.stringify(links.value));
}
</script>

<template>
<MainPage :links="links" @shortenLink="shortenLink"/>
</template>

<style>
body {
    height: 100vh;
}

#app {
    height: 100%;
}
</style>