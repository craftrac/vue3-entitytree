<template>
    <a id="a_toggle_layertreenode_1" href="javascript:;" @click.prevent="toggle">
        <i id="i_layertreenode_1" style="color: black;" :class="iconClass"></i>
    </a>
</template>
<script setup>
import { ref, computed } from 'vue';

const { folded } = defineProps({
  isExpanded: Boolean
});
const emit = defineEmits();
const isExpanded = ref(false);


const toggle = () => {
  isExpanded.value = !isExpanded.value;
  emit('toggle', isExpanded.value); // Emit the 'toggle' event with the new folded value
};

const iconClass = computed(() => {
  return {
    'fa': true,
    'fa-minus': isExpanded.value,
    'fa-plus': !isExpanded.value,
    'color-black': true,
  };
});
</script>