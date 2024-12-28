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
      name: 'John Doe',
      email: 'john.doe@example.com',
      phone: '(555) 123-4567',
      linkedIn: 'linkedin.com/in/johndoe',
      technicalSkills: '',
      softSkills: '',
      workExperience: [
        { company: '', jobTitle: '', years: '' },
      ],
      education: [
        { school: '', diploma: '', years: '' },
      ],
      languages: [
        { language: '', proficiency: '' },
      ],
      interests: [], // Ensure this is an array
    },
  };
},
  methods: {
    updateResumeData(newData) {
      this.resumeData = { ...newData }
    }
  }
}
</script>
