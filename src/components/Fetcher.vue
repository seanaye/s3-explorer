<script setup lang="ts">
import { useFetch } from '@vueuse/core';
import { computed } from 'vue';
import ListView from './ListView.vue'

const { data, isFetching } = useFetch<string>(
  'https://seanaye.nyc3.digitaloceanspaces.com'
);
const xml = computed(() => {
  if (isFetching.value || !data.value) return null;
  console.log('parsing');
  const parser = new DOMParser();
  return parser.parseFromString(data.value, 'application/xml');
});

const selection = computed(() => {
  if (!xml.value) return null

  return xml.value.querySelectorAll("Contents")
})


console.log({ xml, data, isFetching });
</script>
<template>
  <ListView v-if="selection" :list="selection" />
</template>
