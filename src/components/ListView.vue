<script setup lang="ts">
import { computed } from "vue"
import { useBrowserLocation } from "@vueuse/core"
import ListItem  from './ListItem.vue'

const props = defineProps({
  list: {
    type: NodeList,
    required: true
  }
})

export interface ItemData {
    key: string;
}
const location = useBrowserLocation()

const itemData = computed(() => {
  const output: Array<ItemData> = []

  for (let i = 0; i < props.list.length; i += 1) {
    const item = props.list.item(i)
    const children = item?.childNodes
    if (!children) continue

    const toAppend: ItemData = { key: '' } 
    for (let j = 0; j < children.length; j += 1) {
      const data = children.item(j)
      if (j == 0) {
      }
      switch (data.nodeName) {
        case "Key": {
          Object.assign(toAppend, { key: data.textContent })
        }
      }
    }
    if (toAppend.key) {
     output.push(toAppend)
    }
  }

  return output
})

</script>
<template>
    <div class="grid grid-flow-row-dense gap-2 w-screen auto-rows-min">
      <ListItem v-for="item in itemData" :item="item" :key="item.key" :location="location.origin" />
    </div>

</template>
