<template>
    <main>
        <h1>Gerenciar pedidos:</h1>
        <Dashboard />
    </main>
</template>

<script>
import Dashboard from "@/components/Dashboard.vue";

export default {
    name: "Pedidos",
    components: {
        Dashboard
    }
};
</script>


<style lang="less">
main {
    min-height: calc(100vh - 278px)
}
</style>