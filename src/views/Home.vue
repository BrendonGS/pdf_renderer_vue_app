
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
        short_bio: "' is a pseudo-Latin text used in web design, typography, layout, and printing in place of English to emphasise design elements over content. It's also called placeholder (or filler) text. It's a convenient tool for mock-ups. It helps to outline the visual elements of a document or presentation, eg typography, font, or layout. Lorem ipsum is mostly a part of a Latin text by the classical author and philosopher Cicero. Its words and letters have been changed by addition or removal, so to deliberately render its content nonsensical; it's not genuine, correct, or comprehensible Latin anymore. While lorem ipsum's still resembles classical Latin, it actually has no meaning whatsoever.",
        linkedin_url: 'linkedin.com/dylan-cross100',
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
          {
            skill: 'Python',
            student_id: 0
          },
        ],
        experiences: [
          {
            start_date: '2019-03-07',
            end_date: '2019-03-07',
            job_title: 'This Project',
            company_name: 'Actualize',
            details: "is a pseudo-Latin text used in web design, typography, layout, and printing in place of English to emphasise design elements over content. It's also called placeholder (or filler) text. It's a convenient tool for mock-ups. It helps to outline the visual elements of a document or presentation, eg typography, font, or layout. Lorem ipsum is mostly a part of a Latin text by the classical author and philosopher Cicero. Its words and letters have been changed by addition or removal, so to deliberately render its content nonsensical; it's not genuine, correct, or comprehensible Latin anymore. While lorem ipsum's still resembles classical Latin, it actually has no meaning whatsoever.",
            student_id: 0
          }, 
          {
            start_date: '2019-03-07',
            end_date: '2019-03-07',
            job_title: 'My Old Job',
            company_name: 'The One Place',
            details: " is a pseudo-Latin text used in web design, typography, layout, and printing in place of English to emphasise design elements over content. It's also called placeholder (or filler) text. It's a convenient tool for mock-ups. It helps to outline the visual elements of a document or presentation, eg typography, font, or layout. Lorem ipsum is mostly a part of a Latin text by the classical author and philosopher Cicero. Its words and letters have been changed by addition or removal, so to deliberately render its content nonsensical; it's not genuine, correct, or comprehensible Latin anymore. While lorem ipsum's still resembles classical Latin, it actually has no meaning whatsoever.",
            student_id: 0
          }
        ],
        educations: [
          {
            start_date: '2019-03-07',
            end_date: '2019-03-07',
            degree: 'Masters In Everything',
            university_name: 'University of Book Learnin\'',
            details: 'Learned the rest of the things.', 
            student_id: 0
          },
          {
            start_date: '2019-03-07',
            end_date: '2019-03-07',
            degree: 'High School Diploma',
            university_name: 'High School High',
            details: 'Learned some of the things.', 
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
    axios.get('https://kill-nil.herokuapp.com/api/students/' + this.$route.params.id)
      .then(response => {
        console.log(response.data)
        this.resumeParts = response.data
      });
  },
  methods: {
    createPDF () {
        var doc = new jsPDF();
        var pagewidth = 210
        var pageHeight = 297
        var pageCenter = pagewidth / 2
        var nextY = 23
        var bioLines = this.resumeParts['short_bio'].length / 70
        // 4 mm per 12p line 

        doc.setFontSize(20);
        doc.setFont('times', 'bold');
        doc.text((this.resumeParts['first_name'] + ' ' + this.resumeParts['last_name']), pageCenter, nextY, {align: 'center'});
        nextY += 9
        
        doc.setFontSize(12);
        doc.setFont('times', 'normal');
        doc.text(this.resumeParts['email'] + " • " + this.resumeParts['phone_number'], pageCenter, nextY, {align: 'center'});
        nextY += 7
        doc.text(this.resumeParts['github_url'] + " • " + this.resumeParts['linkedin_url'], pageCenter, nextY, {align: 'center'});
        nextY += 5

        doc.line(15, nextY, (pagewidth - 15), nextY);
        nextY += 8

        doc.setFontSize(16);
        doc.setFont('times', 'bold');
        doc.text('Software Developer', pageCenter, nextY, {align: 'center'});
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

        doc.text(skillString, pageCenter, nextY, {align: 'center'});
        nextY += 9;

        doc.setFontSize(16);
        doc.setFont('times', 'bold');
        doc.text('Experience', 14, nextY);
        nextY += 5;

        for (var i = this.resumeParts['experiences'].length - 1; i >= 0; i--) {
          var descLines = this.resumeParts['experiences'][i]['details'].length / 60
          doc.setFontSize(12);
          doc.setFont('times', 'bold');
          doc.text((this.resumeParts['experiences'][i]['company_name'] + ', ' + this.resumeParts['experiences'][i]['job_title']), 14, nextY);
          doc.text((this.resumeParts['experiences'][i]['start_date'] + ' - ' + this.resumeParts['experiences'][i]['end_date']), pagewidth - 14, nextY, {align: 'right'});
          nextY += 5;

          doc.setFont('times', 'normal');
          doc.text(' • ' + this.resumeParts['experiences'][i]['details'], 24, nextY, {maxWidth: (pagewidth - 36)});
          nextY += descLines * 4;
        }

        doc.setFontSize(16);
        doc.setFont('times', 'bold');
        doc.text('Education', 14, nextY);
        nextY += 5;

        for (var i = this.resumeParts['educations'].length - 1; i >= 0; i--) {
          doc.setFontSize(12);
          doc.setFont('times', 'bold');
          doc.text((this.resumeParts['educations'][i]['university_name'] + ', ' + this.resumeParts['educations'][i]['degree']), 14, nextY);
          doc.text((this.resumeParts['educations'][i]['start_date'] + ' - ' + this.resumeParts['educations'][i]['end_date']), pagewidth - 14, nextY, {align: 'right'});
          nextY += 5
          doc.setFontSize(12);
          doc.setFont('times', 'normal');
          doc.text(' • ' + this.resumeParts['educations'][i]['details'], 19, nextY, {maxWidth: (pagewidth - 36)});
          nextY += 5;
        }


        doc.save(this.resumeParts['first_name'] + '_' + this.resumeParts['last_name'] + "_resume" + '.pdf');
    }
  }
}
</script>

