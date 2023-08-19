<template>
  <div class="user-container">
    <h1>User List</h1>
    <div v-for="user in users" :key="user.id" class="user-card">
      <div class="user-card-content">
        <div class="user-avatar">
          <img :src="getUserImage(user.id)" alt="User Avatar" class="user-avatar-img" />
        </div>
        <div class="user-details">
          <h2>{{ user.name }}</h2>
          <p>{{ user.email }}</p>
        </div>
        <div class="view-button">
          <button class="view-button" @click="viewUserPosts(user.id)">View Posts</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      users: '',
    }
  },
  async mounted() {
    this.users = await $fetch('https://jsonplaceholder.typicode.com/users')
  },

  methods: {
    getUserImage(userId) {
      return `https://i.pravatar.cc/150?u=${userId}`; // Using pravatar.cc for example avatars
    },
    viewUserPosts(userId) {
      this.$router.push(`/posts/${userId}`);
    },
  },
};
</script>

<style scoped>
.user-container {
  max-width: 1180px;
  margin: 0 auto;
  padding: 20px;
}

.user-card {
  background-color: #fff;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  border-radius: 8px;
  margin-bottom: 20px;
  overflow: hidden;
}

.user-card-content {
  display: flex;
  align-items: center;
  padding: 15px;
}

.user-avatar {
  width: 50px;
  height: 50px;
  border-radius: 50%;
  overflow: hidden;
  margin-right: 15px;
}

.user-avatar-img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.user-details {
  flex: 1;
  display: flex;
  flex-direction: column;
}

.view-button {
  margin-left: auto;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 4px;
  padding: 5px 10px;
  cursor: pointer;
  transition: background-color 0.2s ease;
}

.view-button:hover {
  background-color: #0056b3;
}
h2 {
  margin: 0;
  font-size: 1.2rem;
}

p {
  margin: 5px 0;
  color: #555;
}
</style>