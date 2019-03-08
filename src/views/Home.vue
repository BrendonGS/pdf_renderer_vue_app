<template>
  <div class="home">
    <button v-on:click='createPDF()'>Download PDF</button>
  </div>
</template>

<script>
// @ is an alias to /src
import jsPDF from 'jspdf';
var axios = require('axios')

export default {
  data: function() {
    return {
      resumeParts: {
        first_name: 'Dylan',
        last_name: 'Cross',
        email: 'dylancross100@gmail.com',
        phone_number: '312-468-1383',
        short_bio: "'Hi! My name is Dylan! This is information. Blah blah blah. This is a middle bio section to push the limits of how the document renders text inside its box. I hope this is long enough because I am getting kind of board of typing. Clearly I need to add just a little bit more. Lets see if this is enough now. I probably should have just added one of those Ipsom Lorem things that these usually use' So now If I add a ton ",
        linked_in_url: 'linkedin.com/dylan-cross100',
        twitter_handle: 'N/A',
        personal_blog: 'dylanswebsite.com',
        resume_url: 'linktomyresume.com',
        github_url: 'github.com/centerpush',
        photo: 'Placeholder',
        // title: 'Software Developer', // *****THIS IS A TEMPORARY FIELD PENDING API APROVAL*****
        skills: [
          {
            skill: 'Ruby',
            student_id: 0
          },
          {
            skill: 'Rails',
            student_id: 0
          },
        ],
        experiences: [
          {
            start_date: '2019-03-07',
            end_date: '2019-03-07',
            job_title: 'This Project',
            company_name: 'Actualize',
            details: 'Built the thing we are working with',
            student_id: 0
          }, 
          {
            start_date: '2019-03-07',
            end_date: '2019-03-07',
            job_title: 'This Project',
            company_name: 'Actualize',
            details: 'Built the thing we are working with',
            student_id: 0
          }
        ],
        educations: [
          {
            start_date: '2019-03-07',
            end_date: '2019-03-07',
            degree: 'Masters In Everything',
            university_name: 'University of Book Learnin\'',
            details: 'Learned the Everything', 
            student_id: 0
          }
        ],
        capstone: [
          {
            name: 'The Thing',
            description: 'It is a thing that does stuff with things.',
            url: 'Website.come',
            student_id: 0
          }
        ]
      }
    };
  },
  created: function() {
    // axios.get('https://kill-nil.herokuapp.com/api/students/1')
    //   .then(response => {
    //     console.log(response.data)
    //     this.resumeParts = response.data
    //   });
  },
  methods: {
    createPDF () {
        var doc = new jsPDF();
        var pagewidth = 210
        var pageHeight = 297
        var nextY = 52
        var bioLines = this.resumeParts['short_bio'].length / 60
        // 4 mm per 12p line 

        doc.setFontSize(20);
        doc.setFont('times', 'bold');
        doc.text((this.resumeParts['first_name'] + ' ' + this.resumeParts['last_name']), (pagewidth / 2), 23, {align: 'center'});
        
        doc.setFontSize(12);
        doc.setFont('times', 'normal');
        doc.text(this.resumeParts['email'] + " • " + this.resumeParts['phone_number'], (pagewidth / 2), 32, {align: 'center'});
        doc.text(this.resumeParts['github_url'] + " • " + this.resumeParts['linkedin_url'], (pagewidth / 2), 39, {align: 'center'});

        doc.line(15, 44, (pagewidth - 15), 44);

        doc.setFontSize(16);
        doc.setFont('times', 'bold');
        doc.text('Software Developer', (pagewidth / 2), nextY, {align: 'center'});
        nextY += 6

        doc.setFontSize(12);
        doc.setFont('times', 'normal');
        doc.text(this.resumeParts['short_bio'], 14, nextY, {maxWidth: (pagewidth - 25)});
        nextY += (4 * bioLines);

        var skillString = ''
        this.resumeParts['skills'].forEach(function(item) {
          skillString += (item['skill'] + " | ");
        });
        skillString = skillString.substring(0, skillString.length - 2);

        doc.text(skillString, (pagewidth / 2), nextY, {align: 'center'});
        nextY += 9;

        doc.setFontSize(16);
        doc.setFont('times', 'bold');
        doc.text('Experience', 14, nextY);
        nextY += 5;

        doc.setFontSize(12);
        doc.setFont('times', 'bold');
        doc.text((this.resumeParts['experiences'][0]['company_name'] + ', ' + this.resumeParts['experiences'][0]['job_title']), 14, nextY);
        doc.text((this.resumeParts['experiences'][0]['start_date'] + ' - ' + this.resumeParts['experiences'][0]['end_date']), pagewidth - 14, nextY, {align: 'right'});
        nextY += 5;

        doc.setFont('times', 'normal');
        doc.text(' • ' + this.resumeParts['experiences'][0]['details'], 24, nextY)


        doc.save(this.resumeParts['first_name'] + '_' + this.resumeParts['last_name'] + "_resume" + '.pdf');
    }
  }
}
</script>