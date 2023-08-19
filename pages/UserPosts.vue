<template>
  <div class="user-posts">
    <h1>{{ userName }}'s Posts</h1>
    <div v-for="post in userPosts" :key="post.id" class="post">
      <h2>{{ post.title }}</h2>
      <p>{{ post.body }}</p>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      userName: '',
      userPosts: [],
    };
  },
  async asyncData({ params }) {
    try {
      const userId = params.userId;
      const [userResponse, postsResponse] = await Promise.all([
        axios.get(`https://jsonplaceholder.typicode.com/users/${userId}`),
        axios.get(`https://jsonplaceholder.typicode.com/posts?userId=${userId}`),
      ]);

      const userName = userResponse.data.name;
      const userPosts = postsResponse.data;

      return { userName, userPosts };
    } catch (error) {
      console.error('Error fetching data:', error);
      return { userName: '', userPosts: [] };
    }
  },
};
</script>

<style scoped>
/* Your post styling */
</style>
