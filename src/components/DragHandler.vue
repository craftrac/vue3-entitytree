<template>
    <a class="drag-handler" href="javascript:;" dragable="true" drag-title="Adriatic Sea subregion" @dragstart="dragstart">
        <i class="fa fa-bars"></i>
    </a>
</template>

<script setup>
const dragstart = (e) => {
    const invalid_area = {
                container: null,
                top: 0,
                left: 0,
                right: 0,
                bottom: 0,
            };
    // if (e.target.getAttribute("dragable") === "true") {
    //     e.dataTransfer.setData("text", e.target.id);
    // }
    console.debug(e.target.id);
    invalid_area.container = e.target; //document.getElementById(e.target + "node_" + e.target.id.split("node_")[1]);
    invalid_area.top = invalid_area.container.getBoundingClientRect().top;
    invalid_area.left = invalid_area.container.getBoundingClientRect().left;
    invalid_area.right = invalid_area.left + invalid_area.container.offsetWidth;
    invalid_area.bottom = invalid_area.top + invalid_area.container.offsetHeight;
    setTimeout(() => {
        invalid_area.container.classList.add("valid");
        // this._lock();
    }, 300);
    //drag callback
    if (e.dragCallback) {
        e.dragCallback(e.nodeList[parseInt(e.target.id.split("node_")[1])]);
    }
    /////// ***** ///////
    //draging
    //clone element when drag start
    const id = e.target.id.split("node_")[1];
    let clone = document.getElementById(e.target + 'node_' + id).cloneNode(true);
    clone.style.position = 'absolute';
    clone.style.zIndex = 1000;
    clone.querySelectorAll('div').forEach(el => el.style.backgroundColor = 'grey');
    clone.querySelectorAll('li').forEach(el => el.style.border = 'unset !important');
    clone.style.width = '50vh';
    //clone.querySelector('ul').remove();
    clone.querySelectorAll('.switch').forEach(el => el.remove());
    const rul = document.createElement('ul');
    rul.appendChild(clone);
    const rdiv = document.createElement('div');
    rdiv.appendChild(rul);
    rdiv.classList.add('dragging-element');
    clone = rdiv;

    e.main_container.appendChild(clone);
    /////// ***** ///////
}


</script>