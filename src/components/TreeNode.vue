<script setup lang="ts">
const props = defineProps<{
    item: Item;
    foldedStatus: {
        type: boolean,
        default: false
    }
}>();
</script>

<script lang="ts">
export type Item = {
  name: string;
  children?: Array<Item>;
};

const slotName = 'default';
</script>
<template>
  <div>
    <div>
      <slot :item="props.item" />
    </div>
    <div
      v-for="(child, index) in props.item.children"
      :key="index"
    >
      <TreeNode :item="child" class="node">
        <template #[slotName]="{ item }: { item: Item }">
          <slot :item="item" />
        </template>
      </TreeNode>
    </div>
  </div>
</template>
<style scoped>
:deep() .node {
    margin-left: 24px;
}
</style>