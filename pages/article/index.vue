<script setup>
import { ref } from 'vue';
definePageMeta({
    layout: "vuetify-app",
});
const polishSelection = ref(1);
const changePolishView = () => {

}
</script>

<style>
.article-card {
    position: relative;
}
</style>

<template>
    <div class=" h-screen bg-gray-00">
        <Header />
        <SearchBar />

        <div class="w-full h-full bg-blue d-flex justify-space-evenly article-card">
            <div class="ma-2">
                <ArticleDetail />
            </div>

            <div class="ma-2">
                <PolishViewDetail />
            </div>
        </div>
    </div>
</template>