<template>
    <Navbar />
    <router-view />
    <Footer />
</template>
<script>
import Navbar from "./components/Navbar.vue";
import Footer from "./components/Footer.vue";

export default {
    components: {
        Navbar,
        Footer,
    },
};
</script>
<style lang="less">
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: Helvetica;
}

main {
    margin: 50px;
    min-height: calc(100vh - 700px)
}

h1 {
    text-align: center;
    font-size: 42px;
    margin-bottom: 30px;
    color: #222;
}
</style>
