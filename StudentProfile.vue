<template>
  <div class="page">
    <div class="profile-header">
      <h2>👤 {{ userData.name }}</h2>
      <p>{{ userData.email }}</p>
    </div>

    <div class="section">
      <h2>📚 My Projects ({{ userProjects.length }})</h2>
      <div v-if="userProjects.length === 0" class="empty-state">
        <p>You haven't uploaded any projects yet</p>
      </div>
      <div v-else class="grid">
        <div v-for="project in userProjects" :key="project.id" class="card">
          <div class="badge">{{ project.category }}</div>
          <h3>{{ project.name }}</h3>
          <p>{{ project.description }}</p>
          <p class="date">Uploaded: {{ project.dateUploaded }}</p>
          <div class="actions">
            <button @click="$emit('view-project', project.id)" class="btn btn-small">View</button>
            <button @click="$emit('delete-project', project.id)" class="btn btn-delete">Delete</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    userData: Object,
    userProjects: Array
  },
  emits: ['delete-project', 'view-project']
}
</script>

<style scoped>
.page { animation: slideIn 0.5s ease-out; }

.profile-header {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  padding: 40px;
  border-radius: 15px;
  margin-bottom: 30px;
  text-align: center;
}

.profile-header h2 {
  color: white;
  margin: 0;
  font-size: 2em;
}

.profile-header p {
  color: rgba(255, 255, 255, 0.9);
  margin: 10px 0 0 0;
}

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

.grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  gap: 20px;
}

.card {
  background: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 100%);
  padding: 25px;
  border-radius: 12px;
  border-left: 5px solid #667eea;
}

.card h3 { color: #333; margin-bottom: 10px; }
.card p { color: #666; margin-bottom: 10px; }

.date { font-size: 0.9em; color: #999; }

.badge {
  display: inline-block;
  background: #667eea;
  color: white;
  padding: 5px 12px;
  border-radius: 20px;
  font-size: 0.8em;
  margin-bottom: 10px;
}

.actions {
  display: flex;
  gap: 10px;
  margin-top: 15px;
}

.btn {
  padding: 8px 16px;
  background: #667eea;
  color: white;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  font-size: 0.9em;
}

.btn:hover { background: #764ba2; }

.btn-small { padding: 6px 12px; font-size: 0.85em; }

.btn-delete {
  background: #e74c3c;
}

.btn-delete:hover { background: #c0392b; }

.empty-state { text-align: center; padding: 60px 20px; color: #999; }

@keyframes slideIn {
  from { opacity: 0; transform: translateY(20px); }
  to { opacity: 1; transform: translateY(0); }
}
</style>