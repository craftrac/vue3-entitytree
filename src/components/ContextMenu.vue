<template>
    <a @click="showMenu = !showMenu">
        <i class="fa fa-list-ul"></i>
        <ul v-show="showMenu" class="contextMenu" >
            <li data-node="123" v-for="entry in menuItems">
                <a><i class="icon-class"></i> {{ entry }}</a>
            </li>
            <!-- More menu items... -->
        </ul>
    </a>
</template>
<script setup>
    import { ref } from 'vue';

    const { menuItems } = defineProps(['menuItems']);
    const showMenu = ref(false);
</script>
<style scoped>
    .contextMenu {
        position: absolute;
        background-color: aliceblue;
    }
</style>