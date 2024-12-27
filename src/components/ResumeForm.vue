<script>
import { PDFDocument } from 'pdf-lib';

export default {
  // Previous content...
  methods: {
    // Previous methods...
    async exportToPDF() {
      const pdfDoc = await PDFDocument.create();
      const page = pdfDoc.addPage();
      page.drawText(`Name: ${this.formData.name}`);
      page.drawText(`Contact: ${this.formData.contact}`, { y: page.getHeight() - 30 });
      // Add other fields...
      const pdfBytes = await pdfDoc.save();
      const blob = new Blob([pdfBytes], { type: 'application/pdf' });
      const link = document.createElement('a');
      link.href = URL.createObjectURL(blob);
      link.download = 'resume.pdf';
      link.click();
    }
  }
};
</script>

<template>
  <!-- Add a button for PDF export -->
  <button @click="exportToPDF">Download as PDF</button>
</template>