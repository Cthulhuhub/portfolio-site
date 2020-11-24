<template>
    <div id="header-ani-container">

    </div>
</template>

<script>
import { onMounted, reactive, onBeforeMount } from 'vue'
import * as PIXI from 'pixi.js'
import {ShockwaveFilter} from '@pixi/filter-shockwave';
export default {
    name: 'HeaderAni',
    setup() {
        const state = reactive({
            app: new PIXI.Application(),
            ticker: {},
            orion: {},
            portrait: {}
        })

        function loadAssets() {
            state.orion = new PIXI.Sprite.from(require('../assets/universe.jpg'))
            state.portrait = new PIXI.Sprite.from(require('../assets/portrait.png'))
            state.app.stage.addChild(state.portrait)
            state.app.stage.addChild(state.orion)
        }

        onBeforeMount(() => {
            loadAssets()
        })

        function initPixi() {
            document.getElementById("header-ani-container").appendChild(state.app.view)
            const parent = state.app.view.parentNode;
            state.app.interactive = true
            const container = new PIXI.Container()

            const background = state.orion

            container.addChild(state.portrait)
            state.app.stage.addChild(container)
            state.app.renderer.resize(parent.clientWidth, parent.clientHeight)

            state.portrait.width = 450
            state.portrait.height = 400
            state.portrait.x = (parent.clientWidth - state.portrait.width) / 2
            state.portrait.y = (parent.clientHeight - state.portrait.height) / 2

            background.width = parent.clientWidth
            background.height = parent.clientHeight

            const wave = new ShockwaveFilter()


            container.filters = [wave]

            state.ticker = PIXI.Ticker.shared
            state.ticker.autoStart = true

            state.ticker.add(() => {
                wave.center = [container.width/2, container.height/2]
                wave.time = (wave.time >= 1 ) ? 0 : wave.time + 0.0017;
                wave.wavelength = 25
                wave.speed = 900
            })
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