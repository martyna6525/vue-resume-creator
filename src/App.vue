<template>
  <div>
    <ResumeForm @form-submitted="updateResumeData" />
    <ResumePreview :data="resumeData" />
  </div>
</template>

<script>
import ResumeForm from './components/ResumeForm.vue';
import ResumePreview from './components/ResumePreview.vue';

export default {
  components: { ResumeForm, ResumePreview },
  data() {
    return {
      resumeData: {}
    };
  },
  methods: {
    updateResumeData(data) {
      this.resumeData = data;
    }
  }
};
</script>