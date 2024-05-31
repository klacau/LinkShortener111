<script setup lang="ts">
import type { ShortLink } from '../models/ShortLink';

import NavigationBar from './NavigationBar.vue';
import ShortLinkList from './ShortLinkList.vue';
import { computed } from 'vue';

interface BasePageProps {
    links: readonly ShortLink[];
}

const props = defineProps<BasePageProps>();

const emit = defineEmits<{
    removeLink: [text: string]
}>();

const innerContentClassList = computed(() => {
    const lst = ['base-page-content-inner'];
    if (props.links.length > 0) {
        if (props.links.length > 1) {
            lst.push('base-page-content-inner--with-list');
        } else {
            lst.push('base-page-content-inner--with-small-list');
        }
    }
    return lst;
});
</script>

<template>
<div class="base-page">
    <NavigationBar />
    <div class="base-page-content">
        <div :class="innerContentClassList.join(' ')">
            <slot></slot>
            
            <div class="base-page__list-wrapper" v-if="props.links.length > 0">
                <ShortLinkList class="base-page__list" 
                    :links="props.links" 
                    @removeLink="shortUrl => $emit('removeLink', shortUrl)" 
                />
            </div>
        </div>
    </div>
</div>
</template>

<style>
.base-page {
    position: relative;
    min-height: 100vh;
    display: flex;
    flex-direction: column;
}

.base-page-content {
    flex-grow: 1;
    display: flex;
    flex-direction: column;
    align-items: stretch;
    justify-content: space-around;
}

.base-page-content-inner--with-list {
    padding-top: 200px;
}

.base-page-content-inner--with-small-list {
    padding-top: 120px;
}

.base-page__list-wrapper {
    margin-top: 56px;
    margin-bottom: 56px;
    display: flex;
    justify-content: space-around;
}

.base-page__list {
    flex-grow: 1;
    width: 100%;
}
</style>
