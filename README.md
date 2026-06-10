# StudentHub - Project Portal (Vue 3)

A complete student project portal built with Vue 3, featuring home page, project listings, project details, upload functionality, student profiles, and admin dashboard.

## 🚀 Features

- **Home Page**: Featured and recent projects with search and category filters
- **Project Listing Page**: Shows all projects with filtering and sorting
- **Project Detail Page**: Full project information with technologies and links
- **Upload Project Page**: Form to submit new projects
- **Student Profile Page**: User's profile and uploaded projects
- **Admin Dashboard**: Review and manage submitted projects

## 📁 Project Structure

```
├── index.html          # Entry HTML file
├── main.js             # Vue app entry point
├── App.vue             # Root component
├── vite.config.js      # Vite configuration
├── package.json        # Dependencies
├── style.css           # Global styles
├── Navigation.vue      # Navigation bar
├── HomePage.vue        # Home page
├── ProjectsPage.vue    # Projects listing
├── ProjectDetail.vue   # Project details
├── UploadProject.vue   # Project upload form
├── StudentProfile.vue  # Student profile
├── AdminDashboard.vue  # Admin panel
└── LoginPage.vue       # Login page
```

## 🛠️ Installation & Setup

### 1. Install Dependencies
```bash
npm install
```

### 2. Run Development Server
```bash
npm run dev
```

The app will open in your browser at `http://localhost:5173`

### 3. Build for Production
```bash
npm run build
```

## 🔐 Login Credentials

The login is simple - just enter:
- **Name**: Any name you want
- **Email**: Any email address
- **Password**: Any password
- **Check "Login as Admin"** if you want admin access

## 📝 How to Use

1. **Login**: First page shows login form
2. **Home**: Browse and search featured projects
3. **Projects**: View all projects with filtering
4. **Upload** (after login): Submit new projects
5. **Profile** (after login): View your uploaded projects
6. **Admin** (admin login): Manage all projects

## 🎨 Features

✅ Real-time search and filtering
✅ Category-based project filtering
✅ Responsive design
✅ Local storage persistence
✅ Admin approval system
✅ Project details with technologies
✅ Student profiles

## 💾 Data Storage

All data is stored in browser's localStorage. Projects and user sessions persist between page refreshes.

## 🤝 Contributing

Feel free to customize and extend this portal!

---

**Built with Vue 3 & Vite** ⚡