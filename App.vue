<template>
  <div id="app">
    <Navigation 
      :current-user="currentUser" 
      :is-admin="isAdmin"
      @show-page="currentPage = $event"
      @logout="logout"
    />

    <div class="main-container">
      <HomePage v-if="currentPage === 'home'" 
        :filtered-projects="filteredProjects"
        :search-query="searchQuery"
        :selected-category="selectedCategory"
        @update-search="searchQuery = $event"
        @update-category="selectedCategory = $event"
        @view-project="viewProjectDetail"
      />

      <ProjectsPage v-if="currentPage === 'projects'"
        :filtered-projects="filteredProjects"
        :search-query="searchQuery"
        :selected-category="selectedCategory"
        @update-search="searchQuery = $event"
        @update-category="selectedCategory = $event"
        @view-project="viewProjectDetail"
      />

      <ProjectDetail v-if="currentPage === 'projectDetail' && selectedProject"
        :project="selectedProject"
        @back="currentPage = 'home'"
      />

      <UploadProject v-if="currentPage === 'upload' && currentUser"
        :current-user="currentUserData"
        @project-uploaded="handleProjectUploaded"
      />

      <StudentProfile v-if="currentPage === 'profile' && currentUser"
        :user-data="currentUserData"
        :user-projects="userProjects"
        @delete-project="deleteProject"
        @view-project="viewProjectDetail"
      />

      <AdminDashboard v-if="currentPage === 'admin' && isAdmin"
        :projects="projects"
        @delete-project="deleteProject"
      />

      <LoginPage v-if="currentPage === 'login' && !currentUser"
        @login="handleLogin"
      />
    </div>
  </div>
</template>

<script>
import { ref, computed } from 'vue'
import Navigation from './Navigation.vue'
import HomePage from './HomePage.vue'
import ProjectsPage from './ProjectsPage.vue'
import ProjectDetail from './ProjectDetail.vue'
import UploadProject from './UploadProject.vue'
import StudentProfile from './StudentProfile.vue'
import AdminDashboard from './AdminDashboard.vue'
import LoginPage from './LoginPage.vue'

export default {
  components: {
    Navigation,
    HomePage,
    ProjectsPage,
    ProjectDetail,
    UploadProject,
    StudentProfile,
    AdminDashboard,
    LoginPage
  },
  setup() {
    const projects = ref([])
    const currentUser = ref(null)
    const isAdmin = ref(false)
    const currentUserData = ref({ name: '', email: '' })
    const currentPage = ref('home')
    const selectedProject = ref(null)
    const searchQuery = ref('')
    const selectedCategory = ref('')

    const filteredProjects = computed(() => {
      return projects.value.filter(p => {
        const nameMatch = p.name.toLowerCase().includes(searchQuery.value.toLowerCase())
        const categoryMatch = selectedCategory.value === '' || p.category === selectedCategory.value
        return nameMatch && categoryMatch
      })
    })

    const userProjects = computed(() => {
      if (!currentUser.value) return []
      return projects.value.filter(p => p.studentEmail === currentUserData.value.email)
    })

    const handleLogin = (userData) => {
      currentUser.value = userData.name
      currentUserData.value = { name: userData.name, email: userData.email }
      isAdmin.value = userData.isAdmin
      currentPage.value = 'home'
      saveToLocalStorage()
    }

    const logout = () => {
      currentUser.value = null
      isAdmin.value = false
      currentPage.value = 'home'
      localStorage.removeItem('currentUser')
    }

    const handleProjectUploaded = (project) => {
      projects.value.push({
        id: Date.now(),
        ...project,
        studentName: currentUserData.value.name,
        studentEmail: currentUserData.value.email,
        dateUploaded: new Date().toLocaleDateString()
      })
      saveProjects()
    }

    const viewProjectDetail = (id) => {
      selectedProject.value = projects.value.find(p => p.id === id)
      currentPage.value = 'projectDetail'
    }

    const deleteProject = (id) => {
      if (confirm('Are you sure?')) {
        projects.value = projects.value.filter(p => p.id !== id)
        saveProjects()
      }
    }

    const saveProjects = () => {
      localStorage.setItem('projects', JSON.stringify(projects.value))
    }

    const loadProjects = () => {
      const saved = localStorage.getItem('projects')
      if (saved) {
        projects.value = JSON.parse(saved)
      }
    }

    const saveToLocalStorage = () => {
      localStorage.setItem('currentUser', JSON.stringify({
        name: currentUserData.value.name,
        email: currentUserData.value.email,
        isAdmin: isAdmin.value
      }))
    }

    const loadFromLocalStorage = () => {
      const saved = localStorage.getItem('currentUser')
      if (saved) {
        const userData = JSON.parse(saved)
        currentUserData.value = { name: userData.name, email: userData.email }
        isAdmin.value = userData.isAdmin
        currentUser.value = userData.name
      }
      loadProjects()
    }

    loadFromLocalStorage()

    return {
      projects,
      currentUser,
      isAdmin,
      currentUserData,
      currentPage,
      selectedProject,
      searchQuery,
      selectedCategory,
      filteredProjects,
      userProjects,
      handleLogin,
      logout,
      handleProjectUploaded,
      viewProjectDetail,
      deleteProject
    }
  }
}
</script>

<style scoped>
#app {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
}

.main-container {
  flex: 1;
  max-width: 1200px;
  margin: 0 auto;
  padding: 20px;
  width: 100%;
}
</style>