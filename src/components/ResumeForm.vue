<template>
    <div class="form-container">
      <h2>Enter your personal information below:</h2>
  
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
          <label for="email">
            <i class="fas fa-envelope"></i> <strong>Email:</strong>
          </label>
          <input
            id="email"
            v-model="editableData.email"
            type="email"
            placeholder="Enter email"
            class="text-input"
            @blur="validateEmail"
          />
          <!-- Error message for invalid email -->
          <span v-if="emailError" class="error-message">Please enter a valid email address.</span>
        </div>
      </div>
  
      <!-- Personal Details Row 2 -->
      <div class="form-row">
        <div class="form-group">
          <label for="phone">
            <i class="fas fa-phone-alt"></i> <strong>Phone:</strong>
          </label>
          <input
            id="phone"
            v-model="editableData.phone"
            type="text"
            placeholder="Enter phone number"
            class="text-input"
          />
        </div>
  
        <div class="form-group">
          <label for="linkedIn">
            <i class="fab fa-linkedin"></i> <strong>LinkedIn:</strong>
          </label>
          <input
            id="linkedIn"
            v-model="editableData.linkedIn"
            type="text"
            placeholder="Enter LinkedIn profile"
            class="text-input"
          />
        </div>
      </div>
  
      <!-- Skills -->
      <div class="form-row">
        <div class="form-group">
          <label for="technicalSkills"><strong>Technical skills:</strong></label>
          <textarea
            id="technicalSkills"
            v-model="editableData.technicalSkills"
            placeholder="Enter technical skills"
            class="text-area"
          ></textarea>
        </div>
  
        <div class="form-group">
          <label for="softSkills"><strong>Soft skills:</strong></label>
          <textarea
            id="softSkills"
            v-model="editableData.softSkills"
            placeholder="Enter soft skills"
            class="text-area"
          ></textarea>
        </div>
      </div>
  
      <!-- Languages and Interests -->
      <div class="form-row">
        <div class="form-group">
          <label for="languages"><strong>Languages:</strong></label>
          <textarea
            id="languages"
            v-model="editableData.languages"
            placeholder="Enter language proficiency"
            class="text-area"
          ></textarea>
        </div>
  
        <div class="form-group">
          <label for="interests"><strong>Interests:</strong></label>
          <textarea
            id="interests"
            v-model="editableData.interests"
            placeholder="Enter interests"
            class="text-area"
          ></textarea>
        </div>
      </div>
  
      <!-- Main Content -->
      <h3>Education</h3>
      <div class="form-group" v-for="(entry, index) in editableData.education" :key="index">
        <label><strong>School {{ index + 1 }}</strong></label>
        <input
          v-model="entry.school"
          type="text"
          placeholder="School name"
          class="text-input"
        />
        <input
          v-model="entry.diploma"
          type="text"
          placeholder="Type of diploma"
          class="text-input"
        />
        <input
          v-model="entry.years"
          type="text"
          placeholder="Years of study (e.g., 2014-2018)"
          class="text-input"
        />
        <button @click="removeEducation(index)" class="cta-button">Remove</button>
      </div>
      <button @click="addEducation" class="cta-button">Add Education</button>

      <div class="form-group">
        <label for="workExperience"><strong>Work experience:</strong></label>
        <textarea
          id="workExperience"
          v-model="editableData.workExperience"
          placeholder="Enter work experience"
          class="text-area"
        ></textarea>
      </div>
  
      <button @click="exportToPDF" class="cta-button" :disabled="emailError">Download as PDF</button>
    </div>
  </template>
  
<script>
import { PDFDocument } from "pdf-lib";

export default {
  props: ["initialData"],
  data() {
    return {
      editableData: { ...this.initialData },
      emailError: false, // Flag to check if email is invalid
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
    async exportToPDF() {
      const pdfDoc = await PDFDocument.create();
      let page = pdfDoc.addPage([600, 400]);

      const fontSize = 12;
      const margin = 20;
      let yPosition = page.getHeight() - margin;

      const fields = [
        `Name: ${this.editableData.name}`,
        `Email: ${this.editableData.email}`,
        `Education:`,
        ...this.editableData.education.map((entry) => `• ${entry.school} - ${entry.diploma} (${entry.years})`),
      ];

      fields.forEach((field) => {
        if (yPosition < margin + fontSize) {
          page = pdfDoc.addPage([600, 400]);
          yPosition = page.getHeight() - margin;
        }
        page.drawText(field, { x: margin, y: yPosition, size: fontSize });
        yPosition -= fontSize + 5;
      });

      const pdfBytes = await pdfDoc.save();
      const blob = new Blob([pdfBytes], { type: "application/pdf" });
      const link = document.createElement("a");
      link.href = URL.createObjectURL(blob);
      link.download = "resume.pdf";
      document.body.appendChild(link);
      link.click();
      document.body.removeChild(link);
    },
  },
};
</script>
