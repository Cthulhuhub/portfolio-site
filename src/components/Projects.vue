<template>
    <h1>Projects</h1>
    <div class="projects-container">
        <div v-for="project in state.projects" class="project-card" :key="project.name">
            <div class="observer-wrapper" :id="`${project.id}`">
            <transition name="slide">
                <div :class="`visibility-wrapper ${project.side}`" v-if="project.visible">
                    <div class="content-wrapper">
                        <div class="project-title">
                            <h3 class="project-name">{{ project.name }}</h3>
                        </div>
                        <div class="project-description">
                            <span>{{ project.description }}</span>
                        </div>
                        <div class="project-links">
                            <span><a :href="project.repo" target="_blank">Github</a> <span v-if="project.site">|</span> <a v-if="project.site" :href="project.site" target="_blank">Site</a></span>
                        </div>
                    </div>
                </div>
            </transition>
            </div>
        </div>
    </div>
</template>

<script>
import { onMounted, reactive } from 'vue'
export default {
    name: 'Projects',
    setup() {
        const state = reactive({
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

        onMounted(() => {
            const projectBoxes = document.querySelectorAll('.observer-wrapper');

            let observer = new IntersectionObserver((entries) => {
                if (entries[0].intersectionRatio <= 0) return;

                entries.forEach(entry => {
                    state.projects[entry.target.id - 1].visible = true
                })
            }, { threshold: 0.8 })

            projectBoxes.forEach(project => {
                observer.observe(project)
            })
        })

        return {
            state
        }
    }
}
</script>

<style scoped>
.projects-container {
    padding-bottom: 75px;
    display: flex;
    flex-direction: column;
    align-content: center;
    justify-content: center;
    width: 100%;
}

.visibility-wrapper {
    transition: all 1s ease;
    display: flex;
    justify-content: center;
    align-items: center;
    margin-top: 20px;
}

.visibility-wrapper:hover {
    transform: scale(1.2, 1.2);
    background-color: white;
    color: rgb(48, 48, 48);
}

.project-name {
    margin-top: 0;
}

.project-title {
    margin-top: 0;
}

.slide-enter-active,
.slide-leave-active {
    transition: all 3s ease;
}

.slide-enter-from,
.slide-leave-to {
    opacity: 0;
}

.slide-enter-from.right,
.slide-leave-to.right {
    opacity: 0;
    transform: translateX(100%);
}

.slide-enter-from.left,
.slide-leave-to.left {
    opacity: 0;
    transform: translateX(-100%);
}

.project-links {
    margin-top: 10px;
}

.project-links a {
    text-decoration: none;
    color: inherit
}

.content-wrapper {
    max-width: 50%;
    margin: 10px;
}

.project-card {
    margin-top: 10px;
}

.observer-wrapper {
    height: 100px;
    width: 100%;
}
</style>