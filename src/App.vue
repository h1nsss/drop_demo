<template>
    <div class="content">
        <div class="drag" ref="drag">
            <div class="drag_box" v-drag></div>
            <img
                class="drag_box"
                src="./assets/1.jpg"
                alt="图片"
                v-drag
                draggable="false"
            />
        </div>
    </div>
</template>

<script>
//引入自定义组件
import "./utils/v-drag";
export default {};
</script>

<style scoped>
.content {
    height: 2000px;
}
.drag {
    width: 100%;
    height: 200px;
    border: 1px solid black;
    background-color: #fff;
    position: relative;
}

.drag_box {
    width: 150px;
    height: 90px;
    /* border: 1px solid #666; */
    background-color: #ccc;
    /* position: absolute; */
    /* top: 100px; */
    /* left: 100px; */
    /* 鼠标移入变成拖拽手势 */
    cursor: move;
    z-index: 3000;
}
</style>