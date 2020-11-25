<template>
    <div id="mobile-carousel-container"></div>
</template>

<script>
import { onMounted, reactive } from 'vue'
import * as PIXI from 'pixi.js'
export default {
    name: "MobileCarousel",
    setup() {
        const state = reactive({
            logos: [
                require('../assets/codeLogos/js.png'),
                require('../assets/codeLogos/react.png'),
                require('../assets/codeLogos/python.png'),
                require('../assets/codeLogos/flask.png'),
                require('../assets/codeLogos/html.png'),
                require('../assets/codeLogos/css.png'),
                require('../assets/codeLogos/vue.png'),
                require('../assets/codeLogos/postgresql.png')
            ],
            app3: {},
            sprites: [],
            containers: [],
            ticker: {},
        })

        function initPixi() {
           state.app3 = new PIXI.Application({
                backgroundColor: 0xFFFFFF
            })
            document.getElementById("mobile-carousel-container").appendChild(state.app3.view)

            const parent = state.app3.view.parentNode;

            state.app3.renderer.resize(parent.clientWidth, parent.clientHeight)

            state.logos.forEach(logo => {
                state.sprites.push(new PIXI.Sprite.from(logo))
            })

            state.sprites.forEach((sprite, i) => {
                let container = new PIXI.Container()
                let spriteContainer = new PIXI.Container()

                container.x = (parent.clientWidth*3 / state.sprites.length)*i

                spriteContainer.addChild(sprite)
                container.addChild(spriteContainer)
                state.app3.stage.addChild(container)
                state.containers.push(container)
            })

            state.app3.view.style.transform = 'scale(1.02, 1)'
            state.ticker = PIXI.Ticker.shared
            state.ticker.autostart = true;

            state.ticker.add(() => {
                state.containers.forEach(container => {
                    container.x = calcPosition(1.33, container.position.x, parent.clientWidth*3, container.width)
                })
            })
        }

         function calcPosition(scr, pos, fullWidth, elWidth) {
            let temp = (scr + pos + fullWidth + elWidth) % fullWidth - elWidth

            return temp
        }

        onMounted(() => {
            initPixi()
        })
    }
}
</script>

<style scoped>
#mobile-carousel-container {
    width: 110%;
    height: 150px;
    margin: 50px 0;
}
</style>