<!-- u18135600 Daniel Stevens -->
<template>
    <div class="Blog" v-if="post">
        <h1>{{ post.title }}</h1>
        <p><strong>Author:</strong> {{ post.author }}</p>
        <p><strong>Category:</strong> {{ post.category }}</p>

        <div class="content" v-html="renderedContent"></div>
    </div>
</template>

<script setup>
import { ref, onMounted } from "vue";
import { useRoute } from "vue-router";
import { marked } from "marked";

const route = useRoute();
const documentId = route.params.documentId;
const post = ref(null);
const renderedContent = ref('');

onMounted(async () => {
    const res = await fetch(`http://localhost:1337/api/posts?filters[documentId][$eq]=${documentId}`);
    const json = await res.json();
    post.value = json.data?.[0] || null;

    renderedContent.value = marked(post.value?.content || '')
})


</script>

<style scoped>
.Blog {
  max-width: 800px;
  margin: auto;
  padding: 1rem;
}
.content {
  margin-top: 2rem;
  line-height: 1.6;
}
</style>