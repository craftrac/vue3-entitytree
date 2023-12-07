<script setup lang="ts">
import { ref, watch } from 'vue';
const props = withDefaults(
  defineProps<{
    item: Item;
    expanded?: boolean;
}>(), {
  expanded: false
});
// const props = 
//   defineProps<{
//     item: Item;
// }>();

const isExpanded = ref(false);


const toggle = (status) => {
  console.debug(status);
  isExpanded.value = status; // Toggle the 'folded' state
};
</script>

<script lang="ts">
export type Item = {
  name: string;
  children?: Array<Item>;
  expanded: boolean;
};

const slotName = 'default';
</script>
<template>
  <ul class="node-list" >
    <li class="node-container">
      <slot :item="props.item" :fold="isExpanded" :toggle="toggle" />
    </li>
    <template 
      v-for="child in item.children"
    >
      <TreeNode :item="child" class="node" v-show="isExpanded" :expanded="isExpanded" >
        <template v-slot="{ item, toggle }: { item: Item; toggle: Function }">
          <slot :item="item" :expanded="isExpanded" />
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