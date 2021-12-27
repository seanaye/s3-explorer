<script setup lang="ts">
import type { PropType } from "vue";
import { computed } from "vue"


const props = defineProps({
  item: {
    type: Object as PropType<{ key: String }>,
    required: true,
  },
  location: {
    type: String,
  }
});

const url = computed(() => `${props.location}/${props.item.key}`)

</script>
<template>
  <a :href="url" v-if="url.includes('NEF')" class="text-blue-500 hover:underline w-48 text-center">{{ item.key }}</a>
</template>

