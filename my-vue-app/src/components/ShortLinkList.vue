<script setup lang="ts">
import type { ShortLink } from '../models/ShortLink';

import { defineProps } from 'vue';
import ShortLinkView from './ShortLinkView.vue';

interface ShortLinkListProps {
    links: readonly ShortLink[];
}

const props = defineProps<ShortLinkListProps>();

const emit = defineEmits<{
    removeLink: [text: string]
}>();
</script>

<template>
  <ul class="short-link-list">
    <li v-for="link in props.links" :key="link.shortUrl" class="link-item">
      <ShortLinkView :shortLink="link" @clickRemove="() => $emit('removeLink', link.shortUrl)" />
    </li>
  </ul>
</template>

<style>
.short-link-list {
  max-width: 776px;
  padding: 4px 24px;
  background-color: #fff;
  border-radius: 20px;
}

.link-item {
  border-bottom: 1px solid #E7EBF3;
}

.link-item:last-of-type {
  border-bottom: none;
}
</style>