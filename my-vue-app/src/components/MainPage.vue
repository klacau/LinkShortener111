<script setup lang="ts">
import type { ShortLink } from '../models/ShortLink';

import Button from './Button.vue';
import InputField from './InputField.vue';
import NavigationBar from './NavigationBar.vue';
import ShortLinkList from './ShortLinkList.vue';
import {ref, computed} from 'vue';

interface MainPageProps {
    links: readonly ShortLink[];
}

const inputText = ref('');

const props = defineProps<MainPageProps>();

const emit = defineEmits<{
    shortenLink: [text: string],
    removeLink: [text: string]
}>();

const innerContentClassList = computed(() => {
    const lst = ['main-page-content-inner'];
    if (props.links.length > 0) {
        if (props.links.length > 1) {
            lst.push('main-page-content-inner--with-list');
        } else {
            lst.push('main-page-content-inner--with-small-list');
        }
    }
    return lst;
});
</script>

<template>
<div class="main-page">
    <NavigationBar />
    <div class="main-page-content">
        <div :class="innerContentClassList.join(' ')">
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
            
            <div class="main-page__list-wrapper" v-if="props.links.length > 0">
                <ShortLinkList class="main-page__list" 
                    :links="props.links" 
                    @removeLink="shortUrl => $emit('removeLink', shortUrl)" 
                />
            </div>
        </div>
    </div>
</div>
</template>

<style>
.main-page {
    position: relative;
    min-height: 100vh;
    display: flex;
    flex-direction: column;
}

.main-page-content {
    flex-grow: 1;
    display: flex;
    flex-direction: column;
    align-items: stretch;
    justify-content: space-around;
}

.main-page-content-inner--with-list {
    padding-top: 200px;
}

.main-page-content-inner--with-small-list {
    padding-top: 120px;
}

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

.main-page__list-wrapper {
    margin-top: 56px;
    margin-bottom: 56px;
    display: flex;
    justify-content: space-around;
}

.main-page__list {
    flex-grow: 1;
    width: 100%;

    
}



.main-page-link{
    display: flex;
    justify-content: space-around;
}
.main-page-link-content{
    flex-grow: 1;
    max-width: 728px;
    max-height: 80px;
}
</style>
