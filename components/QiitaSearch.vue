<template>
    <input type="text" v-model="keyword">
    <div v-if="error">{{ error }}</div>
    <div v-if="status === 'pending'">{{ pending }}Loading...</div>
    <ul>
        <li v-for="item in items"><a v-bind:href="item.url">{{ item.title }}</a></li>
    </ul>
</template>

<script setup lang="ts">
const QIITA_URL = "https://qiita.com/api/v2/items"

const keyword: Ref<string> = ref("")

const query = {
    page: 1,
    per_page: 20,
    query: keyword,
}

const { data: items, error, status } = await useLazyFetch(QIITA_URL, {
    immediate: false,
    query: query,
    watch: [keyword],
})

</script>