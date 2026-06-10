<template>
  <div class="page">
    <button @click="$emit('back')" class="btn back-btn">← Back</button>
    <div class="detail-content">
      <div class="badge">{{ project.category }}</div>
      <h1>{{ project.name }}</h1>
      <p><strong>Student:</strong> {{ project.studentName }}</p>
      <p><strong>Email:</strong> {{ project.studentEmail }}</p>
      <p><strong>Uploaded:</strong> {{ project.dateUploaded }}</p>

      <h3>📝 Description</h3>
      <p class="description">{{ project.description }}</p>

      <h3>🔧 Technologies</h3>
      <div class="technologies">
        <div v-for="tech in project.technologies.split(',')" :key="tech" class="tech-tag">
          {{ tech.trim() }}
        </div>
      </div>

      <h3>🔗 Links</h3>
      <div class="links">
        <a v-if="project.link" :href="project.link" target="_blank" class="link-button">View Live Project</a>
        <a v-if="project.github" :href="project.github" target="_blank" class="link-button">GitHub Repository</a>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    project: Object
  },
  emits: ['back']
}
</script>

<style scoped>
.page { animation: slideIn 0.5s ease-out; }

.back-btn {
  background: #667eea;
  color: white;
  padding: 10px 20px;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  margin-bottom: 20px;
}

.back-btn:hover { background: #764ba2; }

.detail-content {
  background: white;
  padding: 30px;
  border-radius: 15px;
  box-shadow: 0 5px 20px rgba(0, 0, 0, 0.1);
}

.badge {
  display: inline-block;
  background: #667eea;
  color: white;
  padding: 5px 12px;
  border-radius: 20px;
  font-size: 0.8em;
  font-weight: 600;
  margin-bottom: 15px;
}

.detail-content h1 {
  color: #333;
  margin-bottom: 20px;
  font-size: 2.5em;
}

.detail-content h3 {
  color: #333;
  margin-top: 30px;
  margin-bottom: 15px;
  font-size: 1.3em;
  border-bottom: 2px solid #667eea;
  padding-bottom: 10px;
}

.detail-content p {
  color: #666;
  line-height: 1.8;
  margin-bottom: 10px;
}

.description {
  font-size: 1.1em;
  margin: 20px 0;
}

.technologies {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
  margin: 15px 0;
}

.tech-tag {
  background: #e8f1ff;
  color: #667eea;
  padding: 8px 15px;
  border-radius: 20px;
  font-size: 0.95em;
}

.links {
  display: flex;
  gap: 10px;
  flex-wrap: wrap;
  margin-top: 15px;
}

.link-button {
  display: inline-block;
  background: #667eea;
  color: white;
  padding: 10px 20px;
  border-radius: 8px;
  text-decoration: none;
  transition: all 0.3s;
}

.link-button:hover {
  background: #764ba2;
}

@keyframes slideIn {
  from { opacity: 0; transform: translateY(20px); }
  to { opacity: 1; transform: translateY(0); }
}
</style>