<template>
    <header>
        <h1>Make Your Burguer</h1>
    </header>
</template>

<script>
export default {
    name: "Banner",
};
</script>

<style lang="less" scoped>
header {
    background: url("/public/img/burger.jpg");
    background-position: 0 -300px;
    background-size: cover;
    height: 500px;
    display: flex;
    align-items: center;
    justify-content: flex-start;

    h1 {
        color: #fff;
        text-align: center;
        font-size: 60px;
        background-color: #222;
        padding: 20px 40px;
    }
}
</style>
