<script setup lang="ts">
import { defineProps } from 'vue';
import ShortLinkView from './ShortLinkView.vue';
interface ShortLink {
  shortUrl: string;
  originalUrl: string;
}
interface ShortLinkListProps {
  links: ShortLink[];
}

const post = defineProps<ShortLinkListProps>();
</script>

<template>
  <ul>
    <li v-for="link in links" :key="link.shortUrl" class="link-item">
      <ShortLinkView :shortLink="link" />
    </li>
  </ul>
</template>

<style>
</style>