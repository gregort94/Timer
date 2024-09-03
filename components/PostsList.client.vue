<script lang="ts" setup>
type Post = {
  userId: number
  id: number
  title: string
  body: string
}
const { data: posts, status } = await useAsyncData<Post[]>(
  'posts',
  () => $fetch('https://jsonplaceholder.typicode.com/posts'),
  {
    lazy: true,
  }
)
</script>

<template>
  <div>
    <p v-if="status === 'pending'">Posts loading...</p>
    <ul>
      <li v-for="post in posts" :key="post.id">
        <h2>{{ post.title }}</h2>
        <p>{{ post.body }}</p>
      </li>
    </ul>
  </div>
</template>
