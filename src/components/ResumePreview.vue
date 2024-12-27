<template>
    <div class="resume-preview">
      <!-- Header -->
      <header class="resume-header">
        <h1 class="candidate-name">{{ resumeData.name || 'John Doe' }}</h1>
        <div class="contact-info">
          <span v-if="resumeData.email">
            <i class="fas fa-envelope"></i> {{ resumeData.email }}
          </span>
          <span v-if="resumeData.phone">
            <i class="fas fa-phone-alt"></i> {{ resumeData.phone }}
          </span>
          <span v-if="resumeData.linkedIn">
            <i class="fab fa-linkedin"></i> {{ resumeData.linkedIn }}
          </span>
        </div>
      </header>
  
      <div class="resume-content">
        <!-- Left Column -->
        <div class="left-column">
          <!-- Technical Skills -->
          <section class="content-section">
            <h2 class="section-title">Technical skills</h2>
            <ul class="styled-list">
              <li v-for="skill in splitByLines(resumeData.technicalSkills)" :key="skill">{{ skill }}</li>
              <li v-if="!resumeData.technicalSkills">JavaScript</li>
              <li v-if="!resumeData.technicalSkills">HTML</li>
              <li v-if="!resumeData.technicalSkills">CSS</li>
            </ul>
          </section>
  
          <!-- Soft Skills -->
          <section class="content-section">
            <h2 class="section-title">Soft skills</h2>
            <ul class="styled-list">
              <li v-for="skill in splitByLines(resumeData.softSkills)" :key="skill">{{ skill }}</li>
              <li v-if="!resumeData.softSkills">Teamwork</li>
              <li v-if="!resumeData.softSkills">Communication</li>
            </ul>
          </section>
  
          <!-- Languages -->
          <section class="content-section">
            <h2 class="section-title">Languages</h2>
            <ul class="styled-list">
              <li v-for="language in splitByLines(resumeData.languages)" :key="language">{{ language }}</li>
              <li v-if="!resumeData.languages">English (Fluent)</li>
            </ul>
          </section>
        </div>
  
        <!-- Right Column -->
        <div class="right-column">
          <!-- Work Experience -->
          <section class="content-section">
            <h2 class="section-title">Work experience</h2>
            <ul class="styled-list">
              <li v-for="experience in splitByLines(resumeData.workExperience)" :key="experience">{{ experience }}</li>
              <li v-if="!resumeData.workExperience">Software Developer at Tech Solutions</li>
            </ul>
          </section>
  
          <!-- Education -->
          <section class="content-section">
  <h2 class="section-title">Education</h2>
  <ul class="styled-list">
    <li v-for="(entry, index) in resumeData.education" :key="index">
      <div>
        {{ entry.diploma || 'Diploma Type' }}
      </div>
      <div>
        {{ entry.school || 'School Name' }}, {{ entry.years || 'Years of Study' }}
      </div>
    </li>
  </ul>
</section>
    
          <!-- Interests -->
          <section class="content-section">
            <h2 class="section-title">Interests</h2>
            <ul class="styled-list">
              <li v-for="interest in splitByLines(resumeData.interests)" :key="interest">{{ interest }}</li>
              <li v-if="!resumeData.interests">Photography</li>
              <li v-if="!resumeData.interests">Traveling</li>
            </ul>
          </section>
        </div>
      </div>
    </div>
</template>

<script>
export default {
  name: 'ResumePreview',
  props: {
    resumeData: {
      type: Object,
      required: true,
    },
  },
  methods: {
    splitByLines(input) {
      return input ? input.split('\n').filter((line) => line.trim() !== '') : [];
    },
  },
};
</script>
