<template>
  <section id="contact-form">
    <h3 class="box">{{ $t("contactTitle") }}</h3>
    <form
      id="form"
      name="simple-contact-form"
      accept-charset="utf-8"
      action="https://formspree.io/f/xgebbdgn"
      method="POST"
      @submit.prevent="sendEmail"
      class="box"
    >
      <fieldset id="form-inputs">
        <label>Your Name:</label>
        <input type="text" name="name" placeholder="Name" v-model="nameMsg" />
        <label>Your Email:</label>
        <input
          type="email"
          name="_replyto"
          placeholder="abc@abc.com"
          v-model="emailMsg"
        />
        <label>Message:</label>
        <textarea
          name="message"
          rows="15"
          placeholder="Message"
          v-model="messageMsg"
        ></textarea>
      </fieldset>

      <button type="submit" class="btn-submit">
        <DownloadBtn
          :title="'sendMessage'"
          :bgColor="'#fff'"
          :textColor="'#616fe4'"
          :borderColor="'#616fe4'"
          :hoverBgColor="'#616fe4'"
          :hoverTextColor="'#fff'"
          :hoverBorderColor="'#616fe4'"
        />
      </button>
    </form>

    <div class="infos-contact">
      <div class="infos-child box">
        <h5>email</h5>
        <p>betsamene@gmail.com</p>
      </div>
      <div class="infos-child box">
        <h5>current location</h5>
        <p>Madrid - Spain</p>
      </div>
    </div>
    <div v-if="isMessageSent" class="alert-message">
      <p>Your message has been successfully sent!</p>
    </div>
  </section>
</template>

<script>
import axios from "axios";
import gsap from "gsap";
import DownloadBtn from "@/components/DownloadBtn.vue";

export default {
  name: "ContactView",
  components: {
    DownloadBtn,
  },
  data() {
    return {
      nameMsg: "",
      emailMsg: "",
      messageMsg: "",
      isMessageSent: false, // Nueva propiedad para controlar la alerta
    };
  },
  mounted() {
    this.contactAnimation();
  },
  methods: {
    sendEmail() {
      if (!this.nameMsg || !this.emailMsg || !this.messageMsg) {
        // Muestra una alerta indicando que todos los campos deben completarse
        alert("Por favor, complete todos los campos del formulario.");
        return;
      }
      axios
        .post(
          "https://formspree.io/f/xgebbdgn",
          {
            name: this.nameMsg,
            from: this.emailMsg,
            _subject: `${this.nameMsg} | New Message from your website`,
            message: this.messageMsg,
          }
          //  eslint-disable-next-line no-unused-vars
        )
        .then(() => {
          this.isMessageSent = true;
          this.nameMsg = "";
          this.emailMsg = "";
          this.messageMsg = "";
        })
        .catch((error) => {
          if (error.response) {
            // eslint-disable-next-line no-alert
            console.log(error.response.data); // => the response payload
          }
        });
    },
    contactAnimation() {
      gsap.to(".box", {
        stagger: 0.1,
        opacity: 1,
        duration: 1,
        y: 0,
        ease: "power2.inOut",
      });
    },



  },
};
</script>

<style>
#contact-form {
  width: 70%;
  margin: 0 15%;
  padding: 130px 0 50px;
  position: relative;
  z-index: 10;
  display: flex;
  flex-wrap: wrap;
}
#contact-form > h3 {
  font-family: "pp_eikothin", sans-serif;
  font-weight: 200;
  font-size: 5vw;
  line-height: 100%;
  margin: 20px 20px 30px;
  width: 100%;
}
#form {
  display: flex;
  flex-direction: column;
  align-items: flex-end;
  padding: 40px;
}
#form,
.infos-contact {
  width: 50%;
}
fieldset {
  width: 100%;
}
#form-inputs {
  display: flex;
  flex-direction: column;
  margin: 0;
  padding: 0;
  border: none;
}
#form-inputs ::placeholder {
  font-family: "Montserrat", sans-serif;
  padding: 5px;
}
.infos-contact {
  padding: 50px;
  text-align: end;
}
#form-inputs label,
.infos-child > h5 {
  text-transform: uppercase;
  font-size: 14px;
  font-weight: 500;
  font-weight: 600;
  padding-bottom: 8px;
  margin: 0;
}
.infos-child {
  width: 100%;
  display: flex;
  flex-direction: column;
  align-content: flex-end;
}
.infos-child > p {
  height: 50px;
  margin: 0;
}
#form-inputs input {
  height: 50px;
  margin-bottom: 30px;
}
.btn-submit {
  background-color: transparent;
  border: none;
  float: right;
  cursor: pointer;
  margin-top: 20px;
}
.alert-message {
  color: rgb(169, 31, 220);
  padding: 0 32px;
  width: 100%;
}
.box {
  opacity: 0;
  transform: translateY(40px);
}
@media only screen and (max-width: 1024px) {
  #contact-form > h3 {
    font-size: 8vw;
  }
}
@media only screen and (max-width: 768px) {
  #contact-form {
    width: 80%;
    margin: 0 10%;
    flex-direction: column;
    padding: 130px 0 0px;
  }
  #contact-form > h3 {
    padding: 25px;
    margin: 0;
  }
  #form,
  .infos-contact {
    width: 100%;
  }
  .infos-contact {
    text-align: start;
  }
}
@media only screen and (max-width: 480px) {
  #form {
    padding: 20px;
  }
  #contact-form {
    width: 100%;
    margin: 0 auto;
  }
  .infos-contact {
    padding: 0 20px;
    margin-top: 50px;
  }
  .btn-submit {
    width: 100%;
  }
  #contact-form > h3 {
    font-size: 48px;
  }
}
</style>
