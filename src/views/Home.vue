
<template>
  <div class="home">
    <button v-on:click='createPDF'>Download PDF</button>
  </div>
</template>

<script>
// @ is an alias to /src
import jsPDF from 'jspdf';

export default {
  data: function() {
    return {
      resumeParts: {
        // Attributes of the Student Model
        firstName: 'Dylan',
        lastName: 'Cross',
        email: 'dylancross100@gmail.com',
        phoneNumber: '312-468-1383',
        shortBio: 'Hi! My name is Dylan!',
        linkedInURL: 'linkedin.com/dylan-cross100',
        twitterHandle: 'N/A',
        personal: 'dylanswebsite.com', // Blog/Website URL
        onlineResumeUrl: 'linktomyresume.com',
        githubUrl: 'github.com/centerpush',
        photo: 'Placeholder',

        // Each Student will have many:
        // Experience
        experiences: {
          startDate: '2019-03-07',
          endDate: '2019-03-07',
          jobTitle: 'This Project',
          companyName: 'Actualize',
          details: 'Built the thing we are working with'   // (one long text field)
        },
        // Education
        education: {
          startDate: '2019-03-07',
          endDate: '2019-03-07',
          degree: 'Masters In Everything',
          universityName: 'University of Book Learnin\'',
          details: 'Learned the Everything'   // (one long text field)
        },
        // Skills
        skills: {
          skillName: ['Yes', 'Double Yes']  // (E.g. Ruby,HTML,CSS)
        },
        // Capstone
        capstone: {
          name: 'The Thing',
          description: 'It is a thing that does stuff with things.',
          url: 'Website.come',
          screenshot: 'No'
        }



        // // Attributes of the Student Model
        // firstName: '',
        // lastName: '',
        // email: '',
        // phoneNumber: '',
        // shortBio: '',
        // linkedInURL: '',
        // twitterHandle: '',
        // personal: '', // Blog/Website URL
        // onlineResumeUrl: '',
        // githubUrl: '',
        // photo: '',

        // // Each Student will have many:
        // // Experience
        // startDate: '',
        // endDate: '',
        // jobTitle: '',
        // companyName: '',
        // details: '',  // (one long text field)
        // // Education
        // startDate: '',
        // endDate: '',
        // degree: '',
        // universityName: '',
        // details: '',  // (one long text field)
        // // Skills
        // skillName: '', // (E.g. Ruby,HTML,CSS)
        // // Capstone
        // name: '',
        // description: '',
        // url: '',
        // screenshot: ''

      }
    }
  },
  created: function() {},
  methods: {
    createPDF () {
        var pdfName = 'test'; 
        var doc = new jsPDF();
        // doc.setTextColor(0, 255, 0);
        doc.text(this.resumeParts['firstName'], 10, 10);
        doc.text(this.resumeParts['email'], 10, 10);
        doc.text(this.resumeParts['phoneNumber'], 10, 10);
        doc.text(this.resumeParts['shortBio'], 10, 10);
        doc.text(this.resumeParts['linkedInURL'], 10, 10);
        doc.text(this.resumeParts['twitterHandle'], 10, 10);
        doc.text(this.resumeParts['firstName'], 10, 10);
        doc.text(this.resumeParts['firstName'], 10, 10);
        doc.text("Hello World", 10, 10);
        doc.save(pdfName + '.pdf');
      }
  }
}
</script>


<!-- We're stylizing the the resume info in various PDF forms according to our liking  -->