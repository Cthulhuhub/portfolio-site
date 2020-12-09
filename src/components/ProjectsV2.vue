<template>
    <div class="projects-grid">
        <div class="projects-banner">
            <div v-for="(proj, i) in state.projects" :key="i" :id="i+1" class="title-container" @click="handleClick($event)">
                <span class="project-title" :id="i+1">
                    {{proj.name}}
                </span>
            </div>
        </div>
        <div class="projects-descriptions">
            <transition name="projects">
                <div v-if="state.active === 1" class="desc-box">
                    <div class="project-description">
                        <span class="desc-text">{{state.projects[0].description}}</span>
                        <p class="links">
                            <span class="links">
                                <a href="https://github.com/anassri/sprint-turf-project">Github</a> | <a href="https://sprint-turf.herokuapp.com/" target="_blank">Site</a>
                            </span>
                        </p>
                    </div>
                </div>
                <div v-else-if="state.active === 2" class="desc-box">
                    <div class="project-description">
                        <span class="desc-text">{{state.projects[1].description}}</span>
                        <p class="links">
                            <span class="links">
                                <a href="https://github.com/anassri/All-A-Bot">Github</a> | <a href="http://all-a-bot.herokuapp.com/" target="_blank">Site</a>
                            </span>
                        </p>
                    </div>
                </div>
                <div v-else-if="state.active === 3" class="desc-box">
                    <div class="project-description">
                        <span class="desc-text">{{state.projects[2].description}}</span>
                        <p class="links">
                            <span class="links">
                                <a href="https://github.com/Cthulhuhub/battle-blog">Github</a> | <a href="https://battle-blog.herokuapp.com/" target="_blank">Site</a>
                            </span>
                        </p>
                    </div>
                </div>
                <div v-else-if="state.active === 4" class="desc-box">
                    <div class="project-description">
                        <span class="desc-text">{{state.projects[3].description}}</span>
                        <p class="links">
                            <span class="links">
                                <a href="https://github.com/Cthulhuhub/zoom-cord">Github</a>
                            </span>
                        </p>
                    </div>
                </div>
            </transition>
        </div>
        <div class="projects-images">
            <transition name="projects">
                <img v-if="state.active === 1" class="image" :src="require('../assets/projects/sprint-turf.png')" />
                <img v-else-if="state.active === 2" class="image" :src="require('../assets/projects/all-a-bot.png')" />
                <img v-else-if="state.active === 3" class="image" :src="require('../assets/projects/battle-blog.png')" />
                <img v-else-if="state.active === 4" class="image" :src="require('../assets/projects/zoom-cord.png')" />
            </transition>
        </div>
    </div>
</template>

<script>
import { reactive } from 'vue'
export default {
    name: "ProjectsV2",
    setup() {
        const state = reactive({
            active: 1,
            projects: [
                {
                    name: "Sprint Turf",
                    description: "A clone of Remember the Milk that's adapted to the idea of sprint team managment. Has live updating components using pure JavaScript, and styled almost entirely with vanilla CSS.",
                    repo: "https://github.com/anassri/sprint-turf-project",
                    site: "https://sprint-turf.herokuapp.com/",
                    visible: false,
                    id: 1,
                    side: 'left'
                },
                {
                    name: "All A Bot",
                    description: "Uses forms to create JSON objects which are then used to generate simple Discord bots, all on the front end. Bot tokens are never sent across the network to ensure security. Built using React, Flask, and Material UI.",
                    repo: "https://github.com/anassri/All-A-Bot",
                    site: "http://all-a-bot.herokuapp.com/",
                    visible: false,
                    id: 2,
                    side: 'right'
                },
                {
                    name: "Battle Blog",
                    description: "A microblogging site that allows users to have multiple characters, through which they browse the app. Developed with React, Flask, and vanilla CSS.",
                    repo: "https://github.com/Cthulhuhub/battle-blog",
                    site: "https://battle-blog.herokuapp.com/",
                    visible: false,
                    id: 3,
                    side: 'left'
                },
                {
                    name: "Zoom-cord",
                    description: "A Discord bot designed around the App Academy remote program's class structure, making it theoretically possible to use Discord over Zoom and Slack. Made with discord.js.",
                    repo: "https://github.com/Cthulhuhub/zoom-cord",
                    site: '',
                    visible: false,
                    id: 4,
                    side: 'right'
                }
            ]
        })

        function handleClick(e) {
            state.active = parseInt(e.target.id)
        }

        return {
            state,
            handleClick
        }
    }
}
</script>

<style scoped>
.projects-grid {
    display: grid;
    grid-template-rows: 45px 750px;
    grid-template-columns: 2fr 5fr;
    margin: 0 10px;
}

.projects-banner {
    display: flex;
    justify-content: space-around;
    border-top: 1px solid black;
    border-bottom: 1px solid black;
    grid-column-start: 1;
    grid-column-end: 7;
}

.project-title {
    font-size: 25px;
    font-weight: bold;
}

.title-container {
    transition: all 1.25s ease;
    text-align: center;
    width: 100%;
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
}

.title-container:hover {
    transform: scale(1.1);
    background-color: black;
    color: white;
    cursor: pointer;
}

.desc-box {
    position: absolute;
    max-width: 28.57%;
}

.projects-descriptions {
    margin: 10px;
    margin-top: 100px;
    display: flex;
}

.project-description {
    font-size: 20px;
}

.projects-enter-active,
.projects-leave-active {
    transition: all 1.25s ease;
}

.projects-enter-from,
.projects-leave-to {
    opacity: 0;
    transform: scale(0.7, 0.7)
}

/* .image-box {
    position: absolute;
    max-width: 100%;
    max-height: 100%;
} */

.projects-images {
    display: flex;
    justify-content: center;
}

.image {
    max-width: 65%;
    max-height: 750px;
    position: absolute;
}
</style>