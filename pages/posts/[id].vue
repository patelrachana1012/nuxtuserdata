<template>
<div class="user-container">
    <h1>{{ users.name }}'s Posts</h1>
    <div v-for="post in userPosts" :key="post.id" class="post">
      <h4>{{ post.title }}</h4>
      <p>{{ post.body }}</p>
    </div>
</div>
</template>

<script setup>
 const {id} = useRoute().params
 const { data: userPosts} =  await useFetch(`https://jsonplaceholder.typicode.com/posts?userId=${id}`)
 const { data: users} =  await useFetch(`https://jsonplaceholder.typicode.com/users/${id}`)
 console.log(users);
</script>

<style scoped>
.user-container {
  max-width: 1180px;
  margin: 0 auto;
  padding: 20px;
}
</style>
