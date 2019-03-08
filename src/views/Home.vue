<script>
// @ is an alias to /src
import jsPDF from 'jspdf';
var axios = require('axios')

export default {
  data: function() {
    return {
      resumeParts: {
        first_name: '',
        last_name: '',
        email: '',
        phone_number: '',
        short_bio: "",
        linkedin_url: '',
        twitter_handle: '',
        personal_blog: '',
        resume_url: '',
        github_url: '',
        photo: '',
        title: '',
        skills: [],
        experiences: [],
        educations: [],
        capstone: []
      }
    };
  },
  created: function() {
    axios.get('https://kill-nil.herokuapp.com/api/students/' + '2')
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
<<<<<<< HEAD

createPDF()
</script>
=======
</script>

>>>>>>> 65e45676304aa4b02342405df321df84ecd1fceb
