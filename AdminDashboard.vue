<template>
  <div class="page">
    <div class="section">
      <h2>🔧 Admin Dashboard</h2>
      <p>Total Projects: <strong>{{ projects.length }}</strong></p>

      <h3>All Submitted Projects</h3>
      <div v-if="projects.length === 0" class="empty-state">
        <p>No projects submitted yet</p>
      </div>
      <div v-else class="grid">
        <div v-for="project in projects" :key="project.id" class="card">
          <div class="badge">{{ project.category }}</div>
          <h4>{{ project.name }}</h4>
          <p><strong>By:</strong> {{ project.studentName }}</p>
          <p>{{ project.description }}</p>
          <div class="actions">
            <button @click="approve(project.id)" class="btn btn-approve">✓ Approve</button>
            <button @click="$emit('delete-project', project.id)" class="btn btn-delete">✕ Remove</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    projects: Array
  },
  emits: ['delete-project'],
  methods: {
    approve(id) {
      alert('Project approved!')
    }
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

.section h3 {
  color: #333;
  margin: 30px 0 20px 0;
}

.grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  gap: 20px;
}

.card {
  background: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 100%);
  padding: 20px;
  border-radius: 12px;
  border-left: 5px solid #667eea;
}

.card h4 { color: #333; margin: 10px 0; }
.card p { color: #666; margin-bottom: 10px; }

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
  padding: 8px 12px;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  font-size: 0.9em;
  font-weight: 600;
}

.btn-approve {
  background: #27ae60;
  color: white;
}

.btn-approve:hover { background: #229954; }

.btn-delete {
  background: #e74c3c;
  color: white;
}

.btn-delete:hover { background: #c0392b; }

.empty-state { text-align: center; padding: 60px 20px; color: #999; }

@keyframes slideIn {
  from { opacity: 0; transform: translateY(20px); }
  to { opacity: 1; transform: translateY(0); }
}
</style>