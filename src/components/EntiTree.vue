<template>
    <div id="layertree" class="ptree">
        <TreeNode :id="config.key" :item="data" >
          <template v-slot="{ item, toggle }">
            <div class="drop_target" style="color: #2d2d2d">
              <DragHandler class="drag-handler"/>
              <NestToggle class="toggle-handler" v-if="item.children" @toggle="toggle"/>
              {{ item.name }}
              <ContextMenu v-if="item.menu" :menuItems="item.menu"/>
            </div>
          </template>
        </TreeNode>
    </div>
</template>

<style scoped>
@import '../../public/css/style.css';

#layertree {
    background-color: white;
}    
.toggle-handler {
  padding: 10px;
}
.drag-handler {
  padding: 10px;
}
</style>

<script setup>
import myNestedData from '../data/nested-entries.json';
import TreeNode from './TreeNode.vue';
import ContextMenu from './ContextMenu.vue';
import DragHandler from './DragHandler.vue';
import NestToggle from './NestToggle.vue';
import { reactive } from 'vue';


const data = reactive(myNestedData);
const props = defineProps({
    c_data: {
        type: Object,
        required: true
    },
    config: {
        type: Object,
        default: {
            key: new Date().getTime(),
            //logs are open or close
            logMode: false,
            //switch mode
            switchMode: false,
            hasLink: false,
            //family mode
            //for child
            autoChild: true,
            //for parent
            autoParent: true,
            //fold icon
            foldedIcon: "fa fa-plus",
            //unfold icon
            unFoldedIcon: "fa fa-minus",
            //menu icon
            menuIcon: ["fa", "fa-list-ul"],
            //link icon
            linkIcon: "fa fa-list-ul",
            //start status is collapsed or not
            foldedStatus: false,
            //drag
            drag: true,
            //order
            order: false,
            // context menu position
            contextPos: 'after'
        }
    }
});


const test = () => {
    data = [];
    console.log('test');
}
</script>