<template>
    <nav>
        <router-link to="/" id="logo">
            <img src="/img/logo.png" alt="Logo Make Your Burguer" />
        </router-link>
        <router-link to="/">Home</router-link> |
        <router-link to="/pedidos">Pedidos</router-link>
    </nav>
</template>

<script>
export default {
    name: "Navbar",
};
</script>

<style lang="less" scoped>
nav {
    background: #222;
    border-bottom: 4px solid #111;
    padding: 15px 50px;
    display: flex;
    align-items: center;
    justify-content: end;

    #logo {
        margin: auto;
        margin-left: 0;

        img {
            width: 40px;
            height: 40px;
        }
    }

    a {
        color: #fcba03;
        text-decoration: none;
        margin: 12px;
        transition: 0.5s;

        &:hover {
            color: #fff;
        }
    }
}
</style>
