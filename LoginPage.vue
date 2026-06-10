<template>
  <div class="page">
    <div class="login-container">
      <h2>🔐 Login</h2>
      <div v-if="error" class="alert alert-error">{{ error }}</div>
      <form @submit.prevent="submit">
        <div class="form-group">
          <label>Full Name</label>
          <input v-model="form.name" type="text" placeholder="Your name" required>
        </div>
        <div class="form-group">
          <label>Email</label>
          <input v-model="form.email" type="email" placeholder="Your email" required>
        </div>
        <div class="form-group">
          <label>Password</label>
          <input v-model="form.password" type="password" placeholder="Password" required>
        </div>
        <div class="form-group checkbox">
          <input v-model="form.isAdmin" type="checkbox" id="admin">
          <label for="admin">Login as Admin</label>
        </div>
        <button type="submit" class="btn btn-full">Login</button>
      </form>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue'

export default {
  emits: ['login'],
  setup(props, { emit }) {
    const form = ref({
      name: '',
      email: '',
      password: '',
      isAdmin: false
    })
    const error = ref('')

    const submit = () => {
      if (form.value.name && form.value.email && form.value.password) {
        emit('login', { ...form.value })
        form.value = { name: '', email: '', password: '', isAdmin: false }
        error.value = ''
      } else {
        error.value = 'Please fill all fields'
      }
    }

    return { form, error, submit }
  }
}
</script>

<style scoped>
.page {
  display: flex;
  justify-content: center;
  align-items: center;
  animation: slideIn 0.5s ease-out;
}

.login-container {
  background: white;
  padding: 40px;
  border-radius: 15px;
  box-shadow: 0 5px 20px rgba(0, 0, 0, 0.1);
  max-width: 400px;
  width: 100%;
}

.login-container h2 {
  color: #333;
  margin-bottom: 25px;
  text-align: center;
}

.form-group {
  margin-bottom: 20px;
}

.form-group label {
  display: block;
  margin-bottom: 8px;
  color: #333;
  font-weight: 600;
}

.form-group input[type="text"],
.form-group input[type="email"],
.form-group input[type="password"] {
  width: 100%;
  padding: 12px 15px;
  border: 2px solid #e0e0e0;
  border-radius: 8px;
  font-size: 1em;
}

.form-group input[type="text"]:focus,
.form-group input[type="email"]:focus,
.form-group input[type="password"]:focus {
  outline: none;
  border-color: #667eea;
  box-shadow: 0 0 10px rgba(102, 126, 234, 0.1);
}

.form-group.checkbox {
  display: flex;
  align-items: center;
  gap: 10px;
}

.form-group.checkbox input {
  width: auto;
  margin: 0;
}

.form-group.checkbox label {
  margin: 0;
  font-weight: normal;
}

.btn {
  width: 100%;
  padding: 12px;
  background: #667eea;
  color: white;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  font-weight: 600;
  font-size: 1em;
}

.btn:hover { background: #764ba2; }

.btn-full { padding: 12px 20px; }

.alert {
  padding: 12px;
  border-radius: 8px;
  margin-bottom: 20px;
  border-left: 4px solid;
}

.alert-error {
  background: #fadbd8;
  color: #e74c3c;
  border-left-color: #e74c3c;
}

@keyframes slideIn {
  from { opacity: 0; transform: translateY(20px); }
  to { opacity: 1; transform: translateY(0); }
}
</style>