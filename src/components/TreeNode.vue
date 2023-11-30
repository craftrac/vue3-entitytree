<script setup lang="ts">
import { ref } from 'vue';
const props = defineProps<{
    item: Item
}>();

const foldedStatus = ref(false);

const toggleNode = () => {
    console.debug("asasdfasd");
        // let ie = document.getElementById("i_" + node.id);
        // let ule = document.getElementById("c_" + node.id);
        foldedStatus.value = !foldedStatus.value;
        console.debug(foldedStatus.value);
    }
</script>

<script lang="ts">
export type Item = {
  name: string;
  children?: Array<Item>;
};

const slotName = 'default';
</script>
<template>
  <ul class="node-list">
    <li class="node-container">
      <slot :item="props.item" :fold="toggleNode" />
    </li>
    <template 
      v-for="child in props.item.children"
    >
      <TreeNode :item="child" class="node" >
        <template #[slotName]="{ item }: { item: Item }">
            {{ item }}
          <slot :item="item" />
        </template>
      </TreeNode>
    </template>
  </ul>
</template>
<style scoped>
:deep() .node {
    margin-left: 24px;
}
</style>