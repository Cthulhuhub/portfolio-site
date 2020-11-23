<template>
    <div id="header-ani-container">

    </div>
</template>

<script>
import { onMounted, reactive } from 'vue'
import * as PIXI from 'pixi.js'
export default {
    name: 'HeaderAni',
    setup() {
        const state = reactive({
            app: {},
            blackHole: {}
        })

        function initPixi() {
            state.app = new PIXI.Application()
            document.getElementById("header-ani-container").appendChild(state.app.view)
            const parent = state.app.view.parentNode;

            state.app.renderer.resize(parent.clientWidth, parent.clientHeight)
        }

        onMounted(() => {
            initPixi()
        })
    }
}
</script>

<style scoped>
#headeer-ani-container {
    width: 100%;
}
</style>