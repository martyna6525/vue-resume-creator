<template>
    <div v-if="data">
      <h2>Resume Preview</h2>
      <p><strong>Name:</strong> {{ data.name }}</p>
      <p><strong>Contact:</strong> {{ data.contact }}</p>
      <p><strong>Experience:</strong> {{ data.experience }}</p>
      <p><strong>Education:</strong> {{ data.education }}</p>
      <p><strong>Skills:</strong> {{ data.skills }}</p>
    </div>
  </template>
  
  <script>
  export default {
    props: ['data']
  };
  </script>
  
  <style>
  /* Add responsive styling */
  @media (max-width: 600px) {
    div {
      font-size: 14px;
    }
  }
  </style>