<template>
  <div class="home">
    <button v-on:click='createPDF()'>Download PDF</button>
  </div>
</template>

<script>
// @ is an alias to /src
import jsPDF from 'jspdf';

export default {
  data: function() {
    return {
      resumeParts: {
        students: {
          firstName: 'Dylan',
          lastName: 'Cross',
          email: 'dylancross100@gmail.com',
          phoneNumber: '312-468-1383',
          shortBio: 'Hi! My name is Dylan!',
          linkedInURL: 'linkedin.com/dylan-cross100',
          twitterHandle: 'N/A',
          personalBlog: 'dylanswebsite.com',
          resumeUrl: 'linktomyresume.com',
          githubUrl: 'github.com/centerpush',
          photo: 'Placeholder'
        },
        skills: {
          skill: "Yes",
          studentId: 0
        },
        experiences: {
          startDate: '2019-03-07',
          endDate: '2019-03-07',
          jobTitle: 'This Project',
          companyName: 'Actualize',
          details: 'Built the thing we are working with',
          studentId: 0
        },
        educations: {
          startDate: '2019-03-07',
          endDate: '2019-03-07',
          degree: 'Masters In Everything',
          universityName: 'University of Book Learnin\'',
          details: 'Learned the Everything', 
          studentId: 0
        },
        capstone: {
          name: 'The Thing',
          description: 'It is a thing that does stuff with things.',
          url: 'Website.come',
          studentId: 0
        }
      }
      
    }
  },
  created: function() {},
  methods: {
    createPDF () {
        var doc = new jsPDF();
        doc.text(this.resumeParts['students']['firstName'] + ' ' + this.resumeParts['students']['lastName'], 10, 10);
        doc.save(this.resumeParts['students']['firstName'] + '_' + this.resumeParts['students']['lastName'] + "_resume" + '.pdf');
    }
  }
}
</script>
