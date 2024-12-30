<template>
    <div class="form-container">
      <!-- Header with button -->
      <div class="form-header">
        <h2>Enter your personal information below:</h2>
        <button @click="exportToPDF" class="cta-button" :disabled="emailError">Download as PDF</button>
      </div>
  
      <!-- Personal Details Row 1 -->
      <div class="row">
        <div class="form-group">
          <label for="name"><strong>Full name:</strong></label>
          <input
            id="name"
            v-model="editableData.name"
            type="text"
            placeholder="Enter name"
            class="text-input"
          />
        </div>
  
        <div class="form-group">
          <label for="email"><strong>Email:</strong></label>
          <input
            id="email"
            v-model="editableData.email"
            type="email"
            placeholder="Enter email"
            class="text-input"
            @blur="validateEmail"
          />
          <span v-if="emailError" class="error-message">Please enter a valid email address.</span>
        </div>
      </div>
  
      <!-- Personal Details Row 2 -->
      <div class="form-row">
        <div class="form-group">
          <label for="phone"><strong>Phone:</strong></label>
          <input
            id="phone"
            v-model="editableData.phone"
            type="text"
            placeholder="Enter phone number"
            class="text-input"
          />
        </div>
  
        <div class="form-group">
          <label for="linkedIn"><strong>LinkedIn:</strong></label>
          <input
            id="linkedIn"
            v-model="editableData.linkedIn"
            type="text"
            placeholder="Enter LinkedIn profile"
            class="text-input"
          />
        </div>
      </div>
  
      <!-- Education Section -->
      <label><strong>Education</strong></label>
      <div class="form-group" v-for="(entry, index) in editableData.education" :key="index">
        <label><strong>School {{ index + 1 }}</strong></label>
        <input
          v-model="entry.school"
          type="text"
          placeholder="Enter school name"
          class="text-input"
        />
        <label><strong>Type of diploma</strong></label>
        <input
          v-model="entry.diploma"
          type="text"
          placeholder="Enter type of diploma"
          class="text-input"
        />
        <label><strong>Years of study</strong></label>
        <input
          v-model="entry.years"
          type="text"
          placeholder="Enter years of study (e.g., 2015-2020)"
          class="text-input"
        />
        <button @click="removeEducation(index)" class="cta-button">Remove</button>
      </div>
      <button @click="addEducation" class="cta-button">Add Education</button>
  
      <!-- Work Experience Section -->
      <label><strong>Work experience</strong></label>
      <div class="form-group" v-for="(entry, index) in editableData.workExperience" :key="index">
        <label><strong>Work {{ index + 1 }}</strong></label>
        <input
          v-model="entry.company"
          type="text"
          placeholder="Enter company name"
          class="text-input"
        />
        <label><strong>Job Title</strong></label>
        <input
          v-model="entry.jobTitle"
          type="text"
          placeholder="Enter job title"
          class="text-input"
        />
        <label><strong>Years of work</strong></label>
        <input
          v-model="entry.years"
          type="text"
          placeholder="Enter years of work (e.g., 2015-2020)"
          class="text-input"
        />
        <button @click="removeWorkExperience(index)" class="cta-button">Remove</button>
      </div>
      <button @click="addWorkExperience" class="cta-button">Add Work Experience</button>
  
      <!-- Languages Section -->
      <label><strong>Languages</strong></label>
      <div class="form-group" v-for="(entry, index) in editableData.languages" :key="index">
        <label><strong>Language {{ index + 1 }}</strong></label>
        <input
          v-model="entry.language"
          type="text"
          placeholder="Enter language (e.g., English)"
          class="text-input"
        />
        <label><strong>Proficiency Level</strong></label>
        <input
          v-model="entry.proficiency"
          type="text"
          placeholder="Enter proficiency level (e.g., Intermediate)"
          class="text-input"
        />
        <button @click="removeLanguage(index)" class="cta-button">Remove</button>
      </div>
      <button @click="addLanguage" class="cta-button">Add Language</button>
  
      <!-- Interests Section -->
      <label><strong>Interests</strong></label>
      <div class="form-group" v-for="(interest, index) in editableData.interests" :key="index">
        <label><strong>Interest {{ index + 1 }}</strong></label>
        <input
          v-model="editableData.interests[index]"
          type="text"
          placeholder="Enter interest (e.g., Travelling)"
          class="text-input"
        />
        <button @click="removeInterest(index)" class="cta-button">Remove</button>
      </div>
      <!-- Add Interest Button -->
      <button
        v-if="editableData.interests.length < 3"
        @click="addInterest"
        class="cta-button"
      >
        Add Interest
      </button>
    </div>
  </template>
  
  <script>
  export default {
    props: ["initialData"],
    data() {
      return {
        editableData: {
          ...this.initialData,
          education: this.initialData.education || [],
          workExperience: this.initialData.workExperience || [],
          languages: this.initialData.languages || [],
          interests: this.initialData.interests || [], // Ensure default array
        },
        emailError: false,
      };
    },
    methods: {
      validateEmail() {
        const emailPattern = /^[a-zA-Z0-9._-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,6}$/;
        this.emailError = !emailPattern.test(this.editableData.email);
      },
      addEducation() {
        this.editableData.education.push({ school: '', diploma: '', years: '' });
      },
      removeEducation(index) {
        this.editableData.education.splice(index, 1);
      },
      addWorkExperience() {
        this.editableData.workExperience.push({ company: '', jobTitle: '', years: '' });
      },
      removeWorkExperience(index) {
        this.editableData.workExperience.splice(index, 1);
      },
      addLanguage() {
        this.editableData.languages.push({ language: '', proficiency: '' });
      },
      removeLanguage(index) {
        this.editableData.languages.splice(index, 1);
      },
      addInterest() {
        if (this.editableData.interests.length < 3) {
          this.editableData.interests.push(''); // Add an empty string
        }
      },
      removeInterest(index) {
        this.editableData.interests.splice(index, 1); // Remove interest by index
      },
      exportToPDF() {
        console.log("Exporting to PDF...");
      },
    },
  };
  </script>
  