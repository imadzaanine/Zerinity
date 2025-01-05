<template>
    <nav>
        <div class="logo">
            <img src="../assets/logo.png" alt="Logo">
            <h2>Zerepy Framework</h2>
        </div>
        <ul>
            <li v-for="media in medias" :key="media.id">
                <a :href="media.link" target="_blank" rel="noopener noreferrer">
                    <img :src="media.img" alt="Social Media Icon">
                </a>
            </li>
        </ul>
    </nav>
</template>

<script>
export default {
    name: 'AppNavBar', 
    data() {
        return {
            medias: [
                { img: require('../assets/telegram.svg'), link: 'https://www.facebook.com', id: 1 },
                { img: require('../assets/github.svg'), link: 'https://www.github.com', id: 2 },
                { img: require('../assets/youtube.svg'), link: 'https://www.youtube.com', id: 3 },
                { img: require('../assets/twitter.svg'), link: 'https://www.twitter.com', id: 4 },
            ]
        };
    }
};
</script>

<style scoped>
nav {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 1rem 2rem;
}
.logo img {
    width: 100px;
    height: 100px;
}
.logo{
    display: flex;
    align-items: center;
}
ul {
    display: flex;
    list-style: none;
    gap: 30px;
}
li img {
    width: 42px;
    height: 42px;
}
.logo h2 {
    color: #001167;
    font-family: "Inter", sans-serif;
    font-size: 20px;
    font-style: normal;
    font-weight: 500;
    line-height: normal;
}

</style>
