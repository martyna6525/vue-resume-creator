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
  
      <!-- Resume Content -->
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
              <li v-if="!resumeData.softSkills">Problem-solving</li>
            </ul>
          </section>
  
          <!-- Languages -->
          <section class="content-section">
            <h2 class="section-title">Languages</h2>
            <ul class="styled-list">
              <li v-for="(entry, index) in resumeData.languages" :key="index">
                {{ entry.language || 'Language' }} - {{ entry.proficiency || 'Proficiency Level' }}
              </li>
              <li v-if="!resumeData.languages.length">English - Fluent</li>
            </ul>
          </section>
        </div>
  
        <!-- Right Column -->
        <div class="right-column">
          <!-- Work Experience -->
          <section class="content-section">
            <h2 class="section-title">Work experience</h2>
            <ul class="work-education-list">
              <li v-for="(entry, index) in resumeData.workExperience" :key="index">
                <div>
                  <strong>{{ entry.jobTitle || 'Job title' }}</strong>
                </div>
                <div>
                  {{ entry.company || 'Company Name' }}, {{ entry.years || 'Years of work' }}
                </div>
              </li>
              <li v-if="!resumeData.workExperience.length">
                <div>
                  <strong>Software Developer</strong>
                </div>
                <div>Tech Solutions, 2015-2020</div>
              </li>
            </ul>
          </section>
  
          <!-- Education -->
          <section class="content-section">
            <h2 class="section-title">Education</h2>
            <ul class="work-education-list">
              <li v-for="(entry, index) in resumeData.education" :key="index">
                <div>
                  <strong>{{ entry.diploma || 'Diploma type' }}</strong>
                </div>
                <div>
                  {{ entry.school || 'School name' }}, {{ entry.years || 'Years of study' }}
                </div>
              </li>
              <li v-if="!resumeData.education.length">
                <div>
                  <strong>Bachelor's Degree</strong>
                </div>
                <div>University of Tech, 2010-2014</div>
              </li>
            </ul>
          </section>
  
        <!-- Interests Section -->
        <section class="content-section">
        <h2 class="section-title">Interests</h2>
        <ul class="styled-list">
            <li v-for="(interest, index) in resumeData.interests" :key="index">{{ interest || 'New Interest' }}</li>
            <li v-if="!resumeData.interests.length">Photography</li>
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
  