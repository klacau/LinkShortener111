<script setup lang="ts">
import type { ShortLink } from './models/ShortLink';

import MainPage from './components/MainPage.vue';
import { ref, Ref} from 'vue';

const linksValue = localStorage.getItem('links');
const storageLinks: ShortLink[] = linksValue === null ? [] : JSON.parse(linksValue);

const links: Ref<ShortLink[]> = ref(storageLinks);

function shortenLink(text: string) {

    const reg = /((([A-Za-z]{3,9}:(?:\/\/)?)(?:[-;:&=\+\$,\w]+@)?[A-Za-z0-9.-]+|(?:www.|[-;:&=\+\$,\w]+@)[A-Za-z0-9.-]+)((?:\/[\+~%\/.\w-_]*)?\??(?:[-\+=&;%@.\w_]*)#?(?:[\w]*))?)/;

    if (!reg.test(text)) {
        console.error("Это не ссылка")
        return;
    }
    
    const shortenedUrl = `https://localhost:0000/kS9wQ${Math.round(Math.random() * 9999)}`;
    
    const shortLink: ShortLink = {
        shortUrl: shortenedUrl,
        originalUrl: text,
        createdAt: new Date()
    };

    links.value.unshift(shortLink);
    localStorage.setItem('links', JSON.stringify(links.value));
}

function removeLink(shortUrl: string) {
    links.value = links.value.filter(link => link.shortUrl !== shortUrl);
    localStorage.setItem('links', JSON.stringify(links.value));
}
</script>

<template>
<MainPage :links="links" @shortenLink="shortenLink" @removeLink="removeLink" />
</template>

<style>
body {
    height: 100vh;
}

#app {
    height: 100%;
}
</style>