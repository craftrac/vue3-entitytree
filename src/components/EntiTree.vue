<template>
    <div id="layertree" class="ptree">
        <TreeNode :id="config.key" :item="myNestedData">
          <template v-slot="{ item }">
            <div class="drop_target" style="color: #2d2d2d">
              <DragHandler class="drag-handler" />
              <NestToggle class="toggle-handler" v-if="item.children" @click="toggleNode(item)"/>
              {{ item.name }}
            </div>
          </template>
        </TreeNode>
        <ul :id="config.key + '_tree_picklemain'">
          <li></li>
        </ul>
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
import PickleTree from '../ptree.js';
import { onMounted } from 'vue';
import myData from '../data/entries.json';
import myNestedData from '../data/nested-entries.json';
import TreeNode from './TreeNode.vue';
import DragHandler from './DragHandler.vue';
import NestToggle from './NestToggle.vue';


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


onMounted(() => {
    pTree = new PickleTree({
        c_target: 'layertree', //'maptab_treeview',
        c_config: props.config,
        //   switchCallback: layerTreeSwitch,
          c_data: myData
    });
})


const toggleNode = (node) => {
  console.debug(node);
        if (node.children.length > 0) {
            // let ie = document.getElementById("i_" + node.id);
            // let ule = document.getElementById("c_" + node.id);
            if (node.foldedStatus === false) {
              console.debug("ASDASDAS");
                //change icon
                ie.classList.remove("fa-minus");
                ie.classList.add("fa-plus");
                //hide element
                //ule.style.display = "none";
                ule.classList.remove("active");
                ule.classList.add("not-active");
            } else {
                //change icon
                ie.classList.remove("fa-plus");
                ie.classList.add("fa-minus");
                //show element
                //ule.style.display = "";
                ule.classList.remove("not-active");
                ule.classList.add("active");
            }
            node.foldedStatus = !node.foldedStatus;
            //change node status
            for (let key in this.nodeList) {
                if (this.nodeList[key].id === node.id) {
                    this.nodeList[key].foldedStatus = node.foldedStatus;
                }
            }
            this.log("node toggled..");
        } else {
            this.log("node not has childs...!");
        }
    }
</script>