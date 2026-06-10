<template>
  <div class="page">
    <div class="section">
      <h2>⬆️ Upload New Project</h2>
      <div v-if="successMsg" class="alert alert-success">{{ successMsg }}</div>
      <form @submit.prevent="submit">
        <div class="form-row">
          <div class="form-group">
            <label>Project Name *</label>
            <input v-model="form.name" type="text" placeholder="Project name" required>
          </div>
          <div class="form-group">
            <label>Category *</label>
            <select v-model="form.category" required>
              <option value="">Select category</option>
              <option>Web Development</option>
              <option>Mobile App</option>
              <option>Machine Learning</option>
              <option>Data Science</option>
              <option>Desktop App</option>
              <option>Game Development</option>
              <option>IoT</option>
              <option>Other</option>
            </select>
          </div>
        </div>

        <div class="form-group">
          <label>Description *</label>
          <textarea v-model="form.description" placeholder="Describe your project..." required></textarea>
        </div>

        <div class="form-group">
          <label>Technologies Used *</label>
          <input v-model="form.technologies" type="text" placeholder="Vue.js, Node.js, MongoDB" required>
        </div>

        <div class="form-row">
          <div class="form-group">
            <label>Live Link</label>
            <input v-model="form.link" type="url" placeholder="https://...">
          </div>
          <div class="form-group">
            <label>GitHub</label>
            <input v-model="form.github" type="url" placeholder="https://github.com/...">
          </div>
        </div>

        <button type="submit" class="btn btn-full">Upload Project</button>
      </form>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue'

export default {
  props: {
    currentUser: Object
  },
  emits: ['project-uploaded'],
  setup(props, { emit }) {
    const form = ref({
      name: '',
      category: '',
      description: '',
      technologies: '',
      link: '',
      github: ''
    })
    const successMsg = ref('')

    const submit = () => {
      if (form.value.name && form.value.category && form.value.description && form.value.technologies) {
        emit('project-uploaded', { ...form.value })
        form.value = { name: '', category: '', description: '', technologies: '', link: '', github: '' }
        successMsg.value = 'Project uploaded successfully!'
        setTimeout(() => { successMsg.value = '' }, 3000)
      }
    }

    return { form, successMsg, submit }
  }
}
</script>

<style scoped>
.page { animation: slideIn 0.5s ease-out; }

.section {
  background: white;
  padding: 30px;
  border-radius: 15px;
  box-shadow: 0 5px 20px rgba(0, 0, 0, 0.1);
}

.section h2 {
  color: #333;
  margin-bottom: 25px;
  border-bottom: 3px solid #667eea;
  padding-bottom: 15px;
}

.form-row {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 15px;
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

.form-group input,
.form-group select,
.form-group textarea {
  width: 100%;
  padding: 12px 15px;
  border: 2px solid #e0e0e0;
  border-radius: 8px;
  font-size: 1em;
  font-family: inherit;
}

.form-group input:focus,
.form-group select:focus,
.form-group textarea:focus {
  outline: none;
  border-color: #667eea;
  box-shadow: 0 0 10px rgba(102, 126, 234, 0.1);
}

.form-group textarea {
  min-height: 120px;
  resize: vertical;
}

.btn {
  padding: 12px 20px;
  background: #667eea;
  color: white;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  font-weight: 600;
}

.btn:hover { background: #764ba2; }

.btn-full { width: 100%; font-size: 1em; }

.alert {
  padding: 12px;
  border-radius: 8px;
  margin-bottom: 20px;
  border-left: 4px solid;
}

.alert-success {
  background: #d4edda;
  color: #155724;
  border-left-color: #28a745;
}

@keyframes slideIn {
  from { opacity: 0; transform: translateY(20px); }
  to { opacity: 1; transform: translateY(0); }
}

@media (max-width: 768px) {
  .form-row { grid-template-columns: 1fr; }
}
</style>