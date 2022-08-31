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
export default {
    directives: {
        drag: function (el) {
            let dragBox = el; //获取当前元素
            //移动端
            dragBox.ontouchstart = (e) => {
                //算出鼠标相对元素的位置
                let disX = e.touches[0].clientX - dragBox.offsetLeft;
                let disY = e.touches[0].clientY - dragBox.offsetTop;

                //拖拽元素的宽高
                let dragElWidht = dragBox.clientWidth;
                let dragElHight = dragBox.clientHeight;

                let deagParentElWidth = dragBox.parentElement.clientWidth;
                let deagParentEHeight = dragBox.parentElement.clientHeight;

                //阻止冒泡/默认事件
                e.stopPropagation();
                e.preventDefault();

                document.ontouchmove = (e) => {
                    //用鼠标的位置减去鼠标相对元素的位置，得到元素的位置
                    let left = e.touches[0].clientX - disX;
                    let top = e.touches[0].clientY - disY;
                    //边界处理
                    if (left <= 0) {
                        left = 0;
                    }
                    if (left + dragElWidht >= deagParentElWidth) {
                        left = deagParentElWidth - dragElWidht;
                    }
                    if (top <= 0) {
                        top = 0;
                    }
                    if (top + dragElHight >= deagParentEHeight) {
                        top = deagParentEHeight - dragElHight;
                    }
                    //移动当前元素
                    dragBox.style.left = left + "px";
                    dragBox.style.top = top + "px";
                };
                document.ontouchend = (e) => {
                    //鼠标弹起来的时候不再移动
                    document.ontouchmove = null;
                    //预防鼠标弹起来后还会循环（即预防鼠标放上去的时候还会移动）
                    document.ontouchend = null;
                };
            };

            //pc
            dragBox.onmousedown = (e) => {
                //算出鼠标相对元素的位置
                let disX = e.clientX - dragBox.offsetLeft;
                let disY = e.clientY - dragBox.offsetTop;

                //拖拽元素的宽高
                let dragElWidht = dragBox.clientWidth;
                let dragElHight = dragBox.clientHeight;

                let deagParentElWidth = dragBox.parentElement.clientWidth;
                let deagParentEHeight = dragBox.parentElement.clientHeight;

                document.onmousemove = (e) => {
                    //用鼠标的位置减去鼠标相对元素的位置，得到元素的位置
                    let left = e.clientX - disX;
                    let top = e.clientY - disY;
                    //边界处理
                    if (left <= 0) {
                        left = 0;
                    }
                    if (left + dragElWidht >= deagParentElWidth) {
                        left = deagParentElWidth - dragElWidht;
                    }
                    if (top <= 0) {
                        top = 0;
                    }
                    if (top + dragElHight >= deagParentEHeight) {
                        top = deagParentEHeight - dragElHight;
                    }
                    //移动当前元素
                    dragBox.style.left = left + "px";
                    dragBox.style.top = top + "px";
                };
                document.onmouseup = (e) => {
                    //鼠标弹起来的时候不再移动
                    document.onmousemove = null;
                    //预防鼠标弹起来后还会循环（即预防鼠标放上去的时候还会移动）
                    document.onmouseup = null;
                };
            };
        },
    },
};
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
    position: absolute;
    top: 100px;
    left: 100px;
    /* 鼠标移入变成拖拽手势 */
    cursor: move;
    z-index: 3000;
}
</style>