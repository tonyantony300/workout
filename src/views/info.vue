<template>
    <div v-if="dataLoaded" class="container mt-10 px-4">
        <div v-if="data.length === 0" class="w-full flex flex-col items-center">
            <h1 class="text-2xl">Looks empty here...</h1>
        </div>
        <div v-else class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-6">
            <div class="flex flex-col items-center bg-light-grey p-8 shadow-md cursor-pointer"
                v-for="(article, index) in data" :key="index">

                <img src="../assets/images/pencil-light.png" alt=""
                    class="h-24 w-auto" />

                <p class="mt-6 py-1 px-3 text-xs text-white bg-at-light-green shadow-md rounded-lg">
                    {{ article.title }}
                </p>
                <h1 class="mt-8 mb-2 text-center text-xl text-at-light-green">{{ article.publishedAt }}</h1>
            </div>

        </div>

    </div>
</template>
  
<script>
import { ref } from "vue";
export default {
    name: "Info",
    components: {},
    setup() {
        // Create data / vars
        let data = ref([]);
        const dataLoaded = ref(null);
        // Get data
        const getData = async () => {

            try {

               let getNews = await fetch(`https://newsapi.org/v2/top-headlines?country=in&apiKey=6e0d7821ff23471a88e0f1c50d4b5965`)
               data = await getNews.json()
               dataLoaded.value = true;
               console.log(data)
            } catch (e) {
                console.warn(e.message)
            }
        }
        // Run data function
        getData();

        return { data, dataLoaded };
    },
};
</script>