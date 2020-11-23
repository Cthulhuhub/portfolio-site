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
            displacer: {},
            ticker: {}
        })

        function initPixi() {
            state.app = new PIXI.Application()
            document.getElementById("header-ani-container").appendChild(state.app.view)
            const parent = state.app.view.parentNode;
            state.app.interactive = true

            state.app.renderer.resize(parent.clientWidth, parent.clientHeight)

            const img = require('../assets/orion.jpg')
            const background = new PIXI.Sprite.from(img)
            background.width = parent.clientWidth
            background.height = parent.clientHeight
            state.app.stage.addChild(background)

            const portrait = require('../assets/portrait.png')
            const portSprite = new PIXI.Sprite.from(portrait)
            portSprite.width = portSprite.width / 2.5
            portSprite.height = portSprite.height  / 2.5
            portSprite.x = parent.clientWidth / 2 - portSprite.width / 2
            portSprite.y = parent.clientHeight / 2 - portSprite.height / 2
            state.app.stage.addChild(portSprite)

            const displacer = require('../assets/ripple.jpg')
            state.displacer = new PIXI.Sprite.from(displacer)
            let displacementFilter = new PIXI.filters.DisplacementFilter(state.displacer)
            state.app.stage.addChild(state.displacer)
            state.app.stage.filters = [displacementFilter]

            state.app.view.style.transform = 'scale(1.02)'

            state.displacer.scale.x = 1
            state.displacer.scale.y = 1

            state.ticker = PIXI.Ticker.shared
            state.ticker.autoStart = true

            state.ticker.add(() => {
                let mousePos = getMouse()
                state.displacer.x = mousePos.x - (state.displacer.width / 2)
                state.displacer.y = mousePos.y - (state.displacer.height / 2)
            })
        }


        function getMouse() {
            return state.app.renderer.plugins.interaction.mouse.global
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