<template>
  <nav class="navbar">
    <div class="navbar-brand">🎓 StudentHub</div>
    <div class="nav-buttons">
      <button @click="$emit('show-page', 'home')">🏠 Home</button>
      <button @click="$emit('show-page', 'projects')">📚 Projects</button>
      <button v-if="currentUser" @click="$emit('show-page', 'upload')">⬆️ Upload</button>
      <button v-if="currentUser" @click="$emit('show-page', 'profile')">👤 Profile</button>
      <button v-if="isAdmin" @click="$emit('show-page', 'admin')">🔧 Admin</button>
      <button v-if="!currentUser" @click="$emit('show-page', 'login')">🔐 Login</button>
      <button v-else class="logout-btn" @click="$emit('logout')">Logout</button>
    </div>
  </nav>
</template>

<script>
export default {
  props: {
    currentUser: String,
    isAdmin: Boolean
  },
  emits: ['show-page', 'logout']
}
</script>

<style scoped>
.navbar {
  background: white;
  padding: 0 20px;
  height: 70px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
}

.navbar-brand {
  font-size: 1.5em;
  font-weight: bold;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

.nav-buttons {
  display: flex;
  gap: 10px;
}

.nav-buttons button {
  background: none;
  border: none;
  cursor: pointer;
  padding: 10px 15px;
  border-radius: 8px;
  transition: all 0.3s;
  font-size: 0.95em;
}

.nav-buttons button:hover {
  background: #f0f0f0;
}

.logout-btn {
  background: #e74c3c !important;
  color: white;
}

.logout-btn:hover {
  background: #c0392b !important;
}
</style>