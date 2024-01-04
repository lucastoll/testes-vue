<script lang="ts">
    export default {
        data(){
            return{
                windowWidth: window.innerWidth, 
                mobileHeaderActive: false,
            }
        },
        methods: {
            toggleHeader(){
                this.mobileHeaderActive = !this.mobileHeaderActive
            }
        },
        mounted() {
            window.addEventListener('resize', () => this.windowWidth = window.innerWidth);
        },
        unmounted() {
            window.removeEventListener('resize', () => this.windowWidth = window.innerWidth);
        },

    }
</script>

<template>
    <header :style="{ maxHeight: mobileHeaderActive ? '100%' : '80px' }" >
        <div class="imageWrapper">
            <img class="logo" src="../assets/images/logo.svg" alt="VueJS">
            <img class="hamburguer" @click="toggleHeader" v-if="windowWidth < 1024" src="../assets/images/hamburger.png" alt="VueJS">
        </div>
        <nav v-if="windowWidth > 1024 || mobileHeaderActive">
            <ul>
                <li>
                    <a href="#section1">Section1</a>
                </li>
                <li>
                    <a href="#section2">Section2</a>
                </li>
            </ul>
        </nav>
    </header>
</template>

<style scoped>
    header{
        display: flex;
        flex-direction: column;
        justify-content: space-between;
        align-items: center;
        background: #112C27;
        width: 100%;     
        padding: 10px 32px;
        transition: max-height 1s linear;
    }
    .logo {
        width: 80px;
        height: 60px;
    }
    .hamburguer{
        width: 56px;
        height: 27px;
    }
    .imageWrapper{
        width: 100%;
        display: flex;
        justify-content: space-between;
        align-items: center;
    }
    ul{
        display: flex;
        flex-direction: column;
        gap: 16px;
        height: 100%;
        align-items: center;
        padding-bottom: 24px;
    }
    li{
        font-size: 24px;
        font-family: 'HyliaSerif';
        margin: 0;
        padding: 0;
        width: fit-content;
    }
    a{
        text-decoration: none;
        color: white;
    }

    @media screen and (min-width: 1024px){
        header{
            flex-direction: row;
        }
        ul{
            flex-direction: row;
            padding-bottom: 0;
        }
    }
</style>