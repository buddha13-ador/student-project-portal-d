<template>
  <div class="page">
    <div class="hero">
      <h1>🎓 Welcome to StudentHub</h1>
      <p>Discover Amazing Student Projects</p>
    </div>

    <div class="section">
      <h2>🔍 Search Projects</h2>
      <div class="search-container">
        <input 
          :value="searchQuery"
          @input="$emit('update-search', $event.target.value)"
          type="text" 
          placeholder="Search by project name..."
        >
        <select :value="selectedCategory" @change="$emit('update-category', $event.target.value)">
          <option value="">All Categories</option>
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
      <p v-if="searchQuery || selectedCategory" class="search-results">
        Found {{ filteredProjects.length }} project(s)
      </p>
    </div>

    <div class="section">
      <h2>✨ Featured Projects</h2>
      <div v-if="filteredProjects.length === 0" class="empty-state">
        <p>No projects found</p>
      </div>
      <div v-else class="grid">
        <div v-for="project in filteredProjects" :key="project.id" class="card">
          <div class="badge">{{ project.category }}</div>
          <h3>{{ project.name }}</h3>
          <p><strong>By:</strong> {{ project.studentName }}</p>
          <p>{{ project.description }}</p>
          <a v-if="project.link" :href="project.link" target="_blank" class="link-button">View Project 🔗</a>
          <button @click="$emit('view-project', project.id)" class="btn btn-small">View Details</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    filteredProjects: Array,
    searchQuery: String,
    selectedCategory: String
  },
  emits: ['update-search', 'update-category', 'view-project']
}
</script>

<style scoped>
.page {
  animation: slideIn 0.5s ease-out;
}

.hero {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  padding: 60px 30px;
  border-radius: 15px;
  text-align: center;
  margin-bottom: 40px;
}

.hero h1 {
  font-size: 3em;
  margin-bottom: 15px;
}

.section {
  background: white;
  padding: 30px;
  border-radius: 15px;
  margin-bottom: 30px;
  box-shadow: 0 5px 20px rgba(0, 0, 0, 0.1);
}

.section h2 {
  color: #333;
  margin-bottom: 25px;
  font-size: 1.5em;
  border-bottom: 3px solid #667eea;
  padding-bottom: 15px;
}

.search-container {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 15px;
  margin-bottom: 20px;
}

.search-container input,
.search-container select {
  padding: 12px 15px;
  border: 2px solid #e0e0e0;
  border-radius: 8px;
  font-size: 1em;
  transition: all 0.3s;
}

.search-container input:focus,
.search-container select:focus {
  outline: none;
  border-color: #667eea;
  box-shadow: 0 0 10px rgba(102, 126, 234, 0.1);
}

.search-results {
  color: #667eea;
  font-weight: 600;
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
  transition: all 0.3s;
}

.card:hover {
  transform: translateY(-8px);
  box-shadow: 0 15px 35px rgba(0, 0, 0, 0.15);
}

.card h3 {
  color: #333;
  margin-bottom: 10px;
}

.card p {
  color: #666;
  margin-bottom: 10px;
  line-height: 1.6;
}

.badge {
  display: inline-block;
  background: #667eea;
  color: white;
  padding: 5px 12px;
  border-radius: 20px;
  font-size: 0.8em;
  font-weight: 600;
  margin-bottom: 10px;
}

.link-button {
  display: inline-block;
  color: #667eea;
  text-decoration: none;
  margin-right: 10px;
  font-weight: 600;
}

.btn {
  padding: 8px 16px;
  background: #667eea;
  color: white;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  font-size: 0.9em;
  transition: all 0.3s;
}

.btn:hover {
  background: #764ba2;
}

.btn-small {
  padding: 6px 12px;
  font-size: 0.85em;
}

.empty-state {
  text-align: center;
  padding: 60px 20px;
  color: #999;
}

@keyframes slideIn {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@media (max-width: 768px) {
  .search-container {
    grid-template-columns: 1fr;
  }
  .grid {
    grid-template-columns: 1fr;
  }
  .hero h1 {
    font-size: 2em;
  }
}
</style>