<template>
  <div class="app-container">
    <div class="form-section">
      <ResumeForm 
        :initial-data="resumeData" 
        @update:data="updateResumeData" 
      />
    </div>
    <div class="preview-section">
      <ResumePreview :resume-data="resumeData" />
    </div>
    
    <!-- Abstract shapes for background -->
    <div class="shape shape-1"></div>
    <div class="shape shape-2"></div>
    <div class="shape shape-3"></div>
  </div>
</template>

<script>
import ResumeForm from './components/ResumeForm.vue'
import ResumePreview from './components/ResumePreview.vue'

export default {
  name: 'App',
  components: {
    ResumeForm,
    ResumePreview
  },
  data() {
    return {
      resumeData: {
        // Personal Details
        name: '',
        email: '',
        phone: '',
        linkedIn: '',

        // Skills
        technicalSkills: '',
        softSkills: '',
        
        // Languages
        languages: '',
        
        // Main Content
        workExperience: '',
        education: [
          { school: '', diploma: '', years: '' }, // Changed to an array of objects
        ],
        interests: '',
      }
    }
  },
  methods: {
    updateResumeData(newData) {
      this.resumeData = { ...newData }
    }
  }
}
</script>
