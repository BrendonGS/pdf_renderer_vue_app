
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
          shortBio: 'Hi! My name is Dylan! This is information. Blah blah blah. This is a middle bio section to push the limits of how the document renders text inside its box. I hope this is long enough because I am getting kind of board of typing. Clearly I need to add just a little bit more. Lets see if this is enough now. I probably should have just added one of those Ipsom Lorem things that these usually use',
          linkedInUrl: 'linkedin.com/dylan-cross100',
          twitterHandle: 'N/A',
          personalBlog: 'dylanswebsite.com',
          resumeUrl: 'linktomyresume.com',
          githubUrl: 'github.com/centerpush',
          photo: 'Placeholder',
          title: 'Software Developer' // *****THIS IS TEMPORARY FIELD PENDING API APROVAL*****
        },
        skills: {
          skill_label: 'Skills:',
          skill: 'Ruby, TDD, API, TRD, Javascript',
          studentId: 0
        },
        experiences: {
          experiences_label: "Experiences:",
          startDate: '2019-03-07',
          endDate: '2019-03-07',
          jobTitle: 'This Project',
          companyName: 'Actualize',
          details: '• Built the thing we are working with',
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
        var pagewidth = 210
        var pageHeight = 297

        //Student's section

        doc.setFontSize(20);
        doc.setFont('times', 'bold');
        doc.text((this.resumeParts['students']['firstName'] + ' ' + this.resumeParts['students']['lastName']), (pagewidth / 2), 23, {align: 'center'});
        
        doc.setFontSize(12);
        doc.setFont('times', 'normal');
        doc.text(this.resumeParts['students']['email'] + " • " + this.resumeParts['students']['phoneNumber'] + " • " + this.resumeParts['students']['githubUrl'], (pagewidth / 2), 32, {align: 'center'});
        doc.text(this.resumeParts['students']['linkedInUrl'] + " • " + this.resumeParts['students']['twitterHandle'] + " • " + this.resumeParts['students']['resumeUrl'] + " • " + this.resumeParts['students']['personalBlog'], (pagewidth / 2), 39, {align: 'center'});

        doc.line(15, 44, (pagewidth - 15), 44);

        doc.setFontSize(16);
        doc.setFont('times', 'bold');
        doc.text(this.resumeParts['students']['title'], (pagewidth / 2), 52, {align: 'center'});

        doc.setFontSize(12);
        doc.setFont('times', 'normal');
        doc.text(this.resumeParts['students']['shortBio'], 14, 58, {maxWidth: (pagewidth - 25)});

        //end of Student's section



        // Skills section

        doc.setFontSize(14);
        doc.setFont('times');
        doc.text(this.resumeParts['skills']['skill_label'] + "  " + this.resumeParts['skills']['skill'], (pagewidth / 2), 82, {align: 'center'})

        //end of Skills section 



        // Start of experiences section

        doc.setFontSize(16);
        doc.setFont('times', 'bold');
        doc.text(this.resumeParts['experiences']['experiences_label'], 14, 89);

        doc.setFontSize(14);
        doc.setFont('times', 'bold');
        doc.text(this.resumeParts['experiences']['jobTitle'] + ", " + this.resumeParts['experiences']['companyName'], 14, 95);
        doc.text(this.resumeParts['experiences']['startDate'] + " - " + this.resumeParts['experiences']['endDate'], (pagewidth - 12), 95, {align: 'right'});

        doc.setFontSize(14);
        doc.setFont('times');
        doc.text(this.resumeParts['experiences']['details'], 14, 101);



        doc.save(this.resumeParts['students']['firstName'] + '_' + this.resumeParts['students']['lastName'] + "_resume" + '.pdf');
    }
  }
}

</script>


</script>
