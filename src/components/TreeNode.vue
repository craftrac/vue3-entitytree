<script setup lang="ts">
import { ref } from 'vue';
import draggable from 'vuedraggable';

const props = withDefaults(
  defineProps<{
    item: Item;
    expanded?: boolean;
}>(), {
  expanded: false
});

const isExpanded = ref(false);

const toggle = (status) => {
  isExpanded.value = status; // Toggle the 'folded' state
};

const move = (idx) => {
  console.log('peos', idx);
  
}

// function that drags a node in the tree


</script>

<script lang="ts">
export type Item = {
  name: string;
  children?: Array<Item>;
  expanded: boolean;
};

</script>
<template>
  <ul class="node-list" >
    <draggable v-model="props.item" item-key="idx">

    <li class="node-container">
      <slot :item="props.item" :fold="isExpanded" :toggle="toggle" :move="move" />
    </li>
    <template 
      v-for="(child, idx) in item.children" :key="idx"
    >
      <TreeNode :item="child" class="node" v-show="isExpanded" >
        <template v-slot="{ item, toggle }: { item: Item; toggle: Function }">
          <slot :item="item" :toggle="toggle" />
        </template>
      </TreeNode>
    </template>
    </draggable>
  </ul>
</template>
<style scoped>
:deep() .node {
    margin-left: 24px;
}
</style>