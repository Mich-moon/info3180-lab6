<template>
    <ul class="news__list">
        <li v-for="(article, index) in articles" :key="index" class="news__item">  
            <div class="card shadow-sm">
                <img class="card-img-top" :src="article.urlToImage" />

                <div class="card-body">
                    <h4>{{ article.title }}</h4>
                    <p> {{ article.description }} </p>
                </div>
            </div>
        </li>
    </ul>
</template>

<script>
    export default {
        data() {
            return {
                articles: []
            };
        },
        created() {

            let self = this;

            fetch('https://newsapi.org/v2/top-headlines?country=us', 
            {
                headers: {
                'Authorization': `Bearer ${import.meta.env.VITE_NEWSAPI_TOKEN}` 
                }
            })
            .then(function(response) {
            return response.json();
            })
            .then(function(data) {
            console.log(data);

            self.articles = data.articles;

            });
        }
    };
</script>

<style scoped>
.card {
    height:550px;
    border-bottom: 5px solid green;
}
.news__list {
    margin: 0 auto;
    text-align: center;
    list-style: none;
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    grid-gap: 20px;
}
.news__item {
  display: inline-block;
  vertical-align: top;
}
.card-body p {
    text-justify: left;
}
</style>