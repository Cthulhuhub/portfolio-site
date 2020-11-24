<template>
    <div id="logo-carousel-container"></div>
</template>

<script>
import { onMounted, reactive } from 'vue'
import { isMobile } from 'mobile-device-detect'
import * as PIXI from 'pixi.js'
export default {
    name: "LogoCarousel",
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
            app2: {},
            sprites: [],
            containers: [],
            ticker: {},
            moveRate: 0.75,
            scroll: 0,
            displacer: {},
            filter: {},
            direction: 0
        })

        function initPixi() {
            state.app2 = new PIXI.Application({
                backgroundColor: 0xFFFFFF
            })
            document.getElementById("logo-carousel-container").appendChild(state.app2.view)

            const parent = state.app2.view.parentNode;

            state.app2.renderer.resize(parent.clientWidth, parent.clientHeight)

            state.logos.forEach(logo => {
                state.sprites.push(new PIXI.Sprite.from(logo))
            })

            state.sprites.forEach((sprite, i) => {
                let container = new PIXI.Container()
                let spriteContainer = new PIXI.Container()

                if (isMobile) {
                    container.x = 50 * i
                    container.scale(0.5)
                } else {
                    container.x = (parent.clientWidth / state.sprites.length)*i
                }

                spriteContainer.addChild(sprite)
                container.addChild(spriteContainer)
                state.app2.stage.addChild(container)
                state.containers.push(container)
            })

            state.app2.view.style.transform = 'scale(1.02, 1)'
            state.ticker = PIXI.Ticker.shared
            state.ticker.autostart = true;

            addFilter()

            state.ticker.add(() => {
                state.containers.forEach(container => {
                    container.x = calcPosition(state.moveRate, container.position.x, parent.clientWidth, container.width)
                })
                state.filter.scale.x = state.moveRate * 1.75 * -1
            })
        }

        function scrollEvent() {
            document.addEventListener('wheel', e => {
                if (e.deltaY > 0) {
                    state.moveRate += 0.75
                } else if (e.deltaY < 0) {
                    state.moveRate -= 0.75
                }
            })
        }

        function calcPosition(scr, pos, fullWidth, elWidth) {
            let temp = (scr + pos + fullWidth + elWidth) % fullWidth - elWidth

            return temp
        }

        function addFilter() {
            state.displacer = new PIXI.Sprite.from(require('../assets/radiantdisplacer.png'))
            state.app2.stage.addChild(state.displacer)
            state.displacer.width =  state.app2.screen.width
            state.displacer.height =  state.app2.screen.height
            state.displacer.x = (state.app2.screen.width / 2) - (state.displacer.width / 2)
            state.displacer.y = (state.app2.screen.height / 2)  - (state.displacer.height / 1.3)

            state.filter = new PIXI.filters.DisplacementFilter(state.displacer)
            state.filter.scale.set(0)
            state.app2.stage.filters = [state.filter]
        }

        scrollEvent()

        onMounted(() => {
            initPixi()
        })
    }
}
</script>

<style scoped>
#logo-carousel-container {
    width: 110%;
    height: 150px;
    margin: 50px 0;
}
</style>