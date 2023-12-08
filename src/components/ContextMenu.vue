<template>
    <a @click="showMenu = !showMenu">
        <i class="fa fa-list-ul"></i>
        <ul v-show="showMenu" class="contextMenu">
            <li v-for="entry in menuItems">
                <a>{{ entry }}</a>
            </li>
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
        padding-left: 0px;
        position: absolute;
        text-align: left;
        background-color: white;
    }

    .contextMenu li {
        list-style-type: none;
    }

    .contextMenu li:hover {
        background-color: #ef5350;
        color: white;
        cursor: pointer;
    }
</style>