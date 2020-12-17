<template>
<div>
  <div class="container flex-container">
    <img src="../assets/logo.png" class="logo">
    <div class="name_bg">
      <div class="mehfil">
        MEHFIL
      </div>
      <div class="tag_line">
        MEAT WALAN DI
      </div>
    </div>
    <div class="social_media">
      <button class="btn-group" @click="getDirections()">Visit Us</button>
      <button class="btn-group" v-scroll-to="'#contact'">Contact Us</button>
      
    </div>
    <div class="launch_soon">
      Website & Mobile app launching soon.
    </div>
    <div class="stay_tuned">
      STAY TUNED
    </div>
    <div class="contact_form" id="contact">
      <!--Section: Contact v.2-->
      <section class="mb-4">

          <!--Section heading-->
          <h2 class="h1-responsive font-weight-bold text-center my-4">Contact Us</h2>
          <!--Section description-->
          <p class="text-center w-responsive mx-auto mb-5">Do you have any questions? Please do not hesitate to contact us directly. Our team will come back to you within
              matter of minutes to help you.</p>
          <div class="whatsapp">
            <img src="../assets/whatsapp.png" class="whatsapp_image">
            <a href="https://api.whatsapp.com/send?phone=+919897991283">Click here to chat on whatsapp</a>
          </div>

          <div class="or">
            Or write to us by filling following form...
          </div>
          <div class="row">

              <!--Grid column-->
              <div class="col-md-12 mb-md-0 mb-5">
                  <form id="contact-form" name="contact-form" action="mail.php" method="POST">

                      <!--Grid row-->
                      <div class="row custom-row">

                          <!--Grid column-->
                          <div class="col-md-12">
                              <div class="md-form mb-0">
                                  <input type="text" v-model="sender_name" id="name" name="name" class="form-control custom-text" placeholder="Your Name">
                                  
                              </div>
                          </div>
                      </div>
                          <!--Grid column-->
                        <div class="row custom-row">
                          <!--Grid column-->
                          <div class="col-md-12">
                              <div class="md-form mb-0">
                                  <input type="text" v-model="sender_email" id="email" placeholder="Your Email" name="email" class="form-control custom-text">
                                  
                              </div>
                          </div>
                          <!--Grid column-->

                      </div>
                      <!--Grid row-->

                      <!--Grid row-->
                      <div class="row custom-row">
                          <div class="col-md-12">
                              <div class="md-form mb-0">
                                  <input type="text" v-model="sender_subject" id="subject" placeholder="Subject" name="subject" class="form-control custom-text">
                                  
                              </div>
                          </div>
                      </div>
                      <!--Grid row-->

                      <!--Grid row-->
                      <div class="row custom-row">

                          <!--Grid column-->
                          <div class="col-md-12">

                              <div class="md-form">
                                  <textarea type="text" v-model="sender_message" id="message" placeholder="Message" name="message" rows="2" class="form-control md-textarea custom-text"></textarea>
                                  
                              </div>

                          </div>
                      </div>
                      <!--Grid row-->

                  </form>

                  <div class="text-center text-md-left">
                      <div class="message" v-if="this.api_msg.length > 0">{{api_msg}} <span @click="closeMsg()" style="cursor: pointer;">&#10005;</span></div>
                      <div v-if="msg_loader">Sending...</div>
                      <button v-if="!msg_loader" class="btn btn-primary" @click="contact">Send</button>
                  </div>
                  <div class="status"></div>
              </div>

          </div>

      </section>
<!--Section: Contact v.2-->
    </div>
    
    
  </div>
  <div class="footer">
      Designed & Developed with <span style="color: #e25555;">&#9829;</span> by <a href="https://vishalkhare.tech" target="_blank">Vishal Khare</a>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: 'HelloWorld',
  data() {
    return {
      result: [],
      msg_loader : false,
      api_msg : '',
      sender_name: '',
      sender_message: '',
      sender_email: '',
      sender_subject: ''
    };
  },
  methods:{
      getDirections: function () {   
          window.open("https://www.google.com/maps/dir/29.045835,77.687969/mehfil+meat+walan+di/@28.9527275,77.5792111,12z/data=!3m1!4b1!4m9!4m8!1m1!4e1!1m5!1m1!1s0x390c614769c7b3f1:0x379bb7220ebb8601!2m2!1d77.5915259!2d28.8585038", "_blank");    
      },
      scroll: function() {
        const element = document.getElementById('contact');
        element.scrollIntoView({ behavior: 'smooth' });
      },
      closeMsg: function() {
        this.api_msg = '';
      },
      contact: function() {
        this.msg_loader = true;
        if (this.sender_name.length === 0 || this.sender_message.length === 0 || this.sender_email.length === 0 || this.sender_subject.length === 0) {
          this.msg_loader = false;
          this.api_msg = 'All fields are mandatory to submit the form.';
          return;
        }
        axios.post('https://asia-south1-vishalkhare-b30bb.cloudfunctions.net/mehfil-contact',
        {
            message: {
              sender_name: this.sender_name,
              from: this.sender_email,
              subject: this.sender_subject,
              body: this.sender_message
            }
        }).then((response) => {
          console.log(response);
          if (response.data.status) {
            this.api_msg = response.data.msg;
            this.msg_loader = false;
            this.sender_name = '';
            this.sender_email = '';
            this.sender_subject = '';
            this.sender_message = '';
          } else {
            this.api_msg = response.data.msg;
            this.msg_loader = false;
          }
        }, (error) => {
          this.api_msg = 'Something Went wrong...';
          this.msg_loader = false;
          console.log(error);
        });
      }
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.flex-container {
  display: flex;
  justify-content: center;
  flex-direction: column;
}
.logo {
  height: 400px;
  width: 400px;
  margin: auto;
}
.launch_soon {
  margin-top: 1em;
  color: #fff;
  font-size: 3em;
  font-family: 'Raleway', sans-serif;
  line-height: 0.9;
  text-shadow: 5px 5px #ff0000;
  
}
.name_bg {
  color: yellow;
  font-weight: 600;
  width: 400px;
  margin: auto;
  
}
.mehfil {
  line-height: 0.7;
  font-size: 90px;
  text-align: center;
  font-family: 'Raleway', sans-serif;
  text-shadow: 5px 5px #ff0000;
}

.tag_line {
  line-height: 1.2;
  font-size: 40px;
  text-align: center;
  font-family: 'Raleway', sans-serif;
  text-shadow: 5px 5px #ff0000;

}
.svg-class {
  -webkit-filter: invert(100%); /* safari 6.0 - 9.0 */
          filter: invert(100%);
          width: 40px;
          height: 40px;
}
.btn-group {
  background-color: yellow;
  padding: 0.8em;
  padding-right: 1em;
  padding-left: 1em;
  color: #000;
  border: 2px solid #000;
  margin-right: 1em;
  box-shadow: 5px 5px #ff0000;
}
.social_media {
  width: 400px;
  margin: auto;
}
.stay_tuned {
  margin-top: 0.5em;
  margin-bottom: 3em;
  color: #fff;
  font-size: 3.5em;
  font-family: 'Raleway', sans-serif;
  line-height: 0.9;
  text-shadow: 5px 5px #ff0000;
  text-decoration-style: wavy;
}
.contact_form {
  background-color: #fff;
  padding: 2em;
  margin: auto;
  width: 400px;
  color: #000;
  box-shadow: 5px 5px #ff0000;
  margin-bottom: 3em;
}
.custom-row {
  margin-bottom: 1em;
}
.custom-text {
  padding: 1.5em;
}
.footer {
  background-color: #000;
  padding: 1em;
  color: #fff;
}
.footer > a {
  color: #5EF4DA;
  text-decoration: none;
}
.footer > a:hover {
  color: #5EF4DA;
  text-decoration: underline;
}
.whatsapp {
  background-color: yellow;
  padding: 1em;
  box-shadow: 5px 5px #ff0000;
}
.whatsapp_image {
  height: 50px;
  width: 50px;
  margin-right: 1em;
}
.or {
  margin: 1em;
  font-size: 1em;
}
.message {
  padding: 1em;
  background-color: teal;
  color: #fff;
  border-radius: 5px;
  margin-bottom: 1em;
}
</style>
