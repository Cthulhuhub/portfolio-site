<template>
    <div class="footer">
        <div class="left-side">
            <div class="site-info">
                <p class="made-with-text">Made with Vue 3 and PixiJS</p>
                <div class="logo-container">
                    <img class="vue-logo logos" :src="require('../assets/codeLogos/vue.png')" />
                    <img class="pixi-logo logos" :src="require('../assets/codeLogos/pixijs-logo.png')" />
                </div>
            </div>
        </div>
        <div class="right-side">
            <div class="links">
                <p class="linkedin"><a href="https://www.linkedin.com/in/sam-holt-6a47a81bb/" target="_blank">Linkedin</a></p>
                <p class="github"><a href="https://github.com/Cthulhuhub" target="_blank">Github</a></p>
                <p class="email">samuelholt123@gmail.com</p>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "Footer"
}
</script>

<style scoped>
.footer {
    background-color: rgb(48, 48, 48);
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-template-rows: 1fr;
}

.left-side {
    margin: 30px 0;
    border-right: 1px solid rgb(221, 221, 221);
    display: flex;
    flex-direction: column-reverse;
    align-items: flex-start;
}

.right-side {
    margin: 30px 0;
    display: flex;
    flex-direction: column;
    align-items: flex-end;
    text-align: right;
}

.logos {
    width: 100px;
    height: 100px;
}

.vue-logo {
    width: 70px;
    height: 70px;
}

.logo-container {
    display: flex;
    align-items: center;
}

.made-with-text {
    color: rgb(221, 221, 221);
}

.site-info {
    padding-top: 20px;
    margin-left: 20px;
    margin-top: 10px;
}

.links {
    color: rgb(221, 221, 221);
    margin-right: 20px;
    margin-top: 50px;
}

.links a {
    color: rgb(221, 221, 221);
    text-decoration: none;
}

@media only screen and (max-width: 600px) {
    .logos {
        width: 50px;
        height: 50px;
    }

    .vue-logo {
        width: 35px;
        height: 35px;
    }

    .footer {
        font-size: 75%;
    }
}
</style>