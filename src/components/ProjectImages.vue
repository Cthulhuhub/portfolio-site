<template>
    <div class="project-images-container">
        <div class="projects">
            <div class="sprint-turf proj" id="proj-1" @mouseenter="handleEnter" @mouseleave="handleLeave">
                <h2>Sprint Turf</h2>
            </div>
            <div class="all-a-bot proj" id="proj-2" @mouseenter="handleEnter" @mouseleave="handleLeave">
                <h2>All A Bot</h2>
            </div>
            <div class="battle-blog proj" id="proj-3" @mouseenter="handleEnter" @mouseleave="handleLeave">
                <h2>Battle Blog</h2>
            </div>
            <div class="zoom-cord proj" id="proj-4" @mouseenter="handleEnter" @mouseleave="handleLeave">
                <h2>Zoom-cord</h2>
            </div>
        </div>
        <div class="images">
        <transition name="img">
            <div class="img1 img" v-if="state.hover1">
                <img :src="require('../assets/projects/sprint-turf.png')" />
            </div>
            <div class="img2 img" v-else-if="state.hover2">
                <img :src="require('../assets/projects/all-a-bot.png')" />
            </div>
            <div class="img3 img" v-else-if="state.hover3">
                <img :src="require('../assets/projects/battle-blog.png')" />
            </div>
            <div class="img4 img" v-else-if="state.hover4">
                <img :src="require('../assets/projects/zoom-cord.png')" />
            </div>
        </transition>
        </div>
    </div>
</template>

<script>
import { reactive } from 'vue'
export default {
    name: "ProjectImages",
    setup() {
        const state = reactive({
            hover1: false,
            hover2: false,
            hover3: false,
            hover4: false
        })

        function handleEnter(e) {
            switch (e.target.id) {
                case 'proj-1':
                    state.hover1 = true
                    break
                case 'proj-2':
                    state.hover2 = true
                    break
                case 'proj-3':
                    state.hover3 = true
                    break
                case 'proj-4':
                    state.hover4 = true
                    break
            }
        }

        function handleLeave(e) {
            switch (e.target.id) {
                case 'proj-1':
                    state.hover1 = false
                    break
                case 'proj-2':
                    state.hover2 = false
                    break
                case 'proj-3':
                    state.hover3 = false
                    break
                case 'proj-4':
                    state.hover4 = false
                    break
            }
        }

        return {
            state,
            handleEnter,
            handleLeave
        }
    }
}
</script>

<style scoped>
.project-images-container {
    width: 100%;
    display: grid;
    grid-template-columns: 1fr 2fr;
    grid-template-rows: 1fr;
}

.projects {
    margin: 20px 0;
    min-width: 100%;
    display: flex;
    grid-column: 1;
    flex-direction: column;
    text-align: left;

}

.projects h2 {
    margin-left: 25px;
}

.proj {
    transition: all 1s ease;
    padding: 10px;
    border-right: 1px solid rgb(48, 48, 48);
}

.projects div:hover {
    color: rgb(221, 221, 221);
    background-color: rgb(48, 48, 48);
    transform: scale(1.05, 1.05);
    border-right: 1px solid rgb(48, 48, 48);
}

.images {
    max-width: 100%;
    display: flex;
    height: 750px;
    grid-column: 2;
    justify-content: center;
}

.images img {
    max-width: 100%;
    max-height: 750px;
}

.img {
    position: absolute;
}

.img-enter-active,
.img-leave-active {
    transition: all 1.15s ease;
}

.img-enter-from,
.img-leave-to {
    opacity: 0;
    transform: scale(0.7, 0.7)
}
</style>