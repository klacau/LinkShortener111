<script setup lang="ts">
import type { ShortLink } from './models/ShortLink';

import LinkCreatedPage from './components/LinkCreatedPage.vue';
import MainPage from './components/MainPage.vue';
import { ref, Ref } from 'vue';

type Page = 'Main' | 'LinkCreated';

const currentPage = ref<Page>('Main');
const currentLink = ref<ShortLink>();
const hasError = ref<boolean>(false);

const linksValue = localStorage.getItem('links');
const storageLinks: ShortLink[] = linksValue === null ? [] : JSON.parse(linksValue);

const links: Ref<ShortLink[]> = ref(storageLinks);

function shortenLink(text: string) {

    const reg = /((([A-Za-z]{3,9}:(?:\/\/)?)(?:[-;:&=\+\$,\w]+@)?[A-Za-z0-9.-]+|(?:www.|[-;:&=\+\$,\w]+@)[A-Za-z0-9.-]+)((?:\/[\+~%\/.\w-_]*)?\??(?:[-\+=&;%@.\w_]*)#?(?:[\w]*))?)/;

    if (!reg.test(text)) {
        hasError.value = true
        return;
    }
    
    const shortenedUrl = `https://localhost:0000/kS9wQ${Math.round(Math.random() * 9999)}`;
    
    const shortLink: ShortLink = {
        shortUrl: shortenedUrl,
        originalUrl: text,
        createdAt: new Date()
    };

    currentPage.value = 'LinkCreated';
    currentLink.value = shortLink;
    hasError.value = false

    links.value.unshift(shortLink);
    localStorage.setItem('links', JSON.stringify(links.value));
}

function removeLink(shortUrl: string) {
    links.value = links.value.filter(link => link.shortUrl !== shortUrl);
    localStorage.setItem('links', JSON.stringify(links.value));
}
</script>

<template>
<MainPage v-if="currentPage === 'Main'" 
    :links="links" 
    :hasError="hasError"
    @shortenLink="shortenLink" 
    @removeLink="removeLink"
/>
<LinkCreatedPage v-else-if="currentPage === 'LinkCreated'"
    :createdLink="currentLink!"
    :links="links" 
    @shortenAnotherLink="() => { currentPage = 'Main' }" 
    @removeLink="removeLink" 
/>
</template>

<style>
body {
    height: 100vh;
}

#app {
    height: 100%;
}
</style>