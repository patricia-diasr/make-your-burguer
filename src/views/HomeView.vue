<template>
    <Banner />
    <main>
        <h1>Monte o seu burguer</h1>
        <BurgerForm />
    </main>
</template>

<script>
import Banner from "@/components/Banner.vue";
import BurgerForm from "@/components/BurgerForm.vue";

export default {
    name: "Home",
    components: {
        Banner,
        BurgerForm
    },
};
</script>
