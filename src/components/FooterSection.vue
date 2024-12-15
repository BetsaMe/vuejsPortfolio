<template>
  <section id="contact">
    <div class="circle-container-footer">
      <div class="circle5"></div>
      <div class="circle6"></div>
    </div>
    <div class="contact">
      <div class="bloc-contact">
        <p class="footer-info">
          {{ $t("footerParagraph") }}
        </p>
        <router-link to="/contact" v-if="$route.path !== '/contact'">
          <DownloadBtn
            title="contacto"
            :bgColor="'#616fe4'"
            :textColor="'#fff'"
            :borderColor="'#616fe4'"
            :hoverBgColor="'#444444'"
            :hoverTextColor="'#fff'"
            :hoverBorderColor="'#444444'"
          />
        </router-link>

        <div class="ctn-footer-links">
          <ArrowBtn
            href="https://www.linkedin.com/in/betsab%C3%A9-m-4972178b/"
            target="_blank"
            title="Linkedin"
          />
          <ArrowBtn
            href="https://www.behance.net/betsameneses"
            target="_blank"
            title="behance"
          />
          <ArrowBtn
            href="https://github.com/BetsaMe"
            target="_blank"
            title="github"
          />
        </div>
      </div>
    </div>
    <div class="creator">
      <span class="">© {{ new Date().getFullYear() }} Betsabé M</span>
    </div>
  </section>
</template>

<script>
import gsap from "gsap";
import ScrollTrigger from "gsap/ScrollTrigger";
import ArrowBtn from "@/components/ArrowBtn.vue";
import DownloadBtn from "@/components/DownloadBtn.vue";

export default {
  name: "FooterSection",
  components: {
    ArrowBtn,
    DownloadBtn,
  },
  mounted() {
    ScrollTrigger.refresh();
    gsap.registerPlugin(ScrollTrigger);
    this.parallaxContact();
  },
  methods: {
    parallaxContact() {
      let mm = gsap.matchMedia();
      mm.add("(min-width: 800px)", () => {
        gsap.to(".circle5", {
          x: 120,
          scrollTrigger: {
            trigger: ".contact",
            start: "top center+=200",
            scrub: 1,
          },
        });
      });
      mm.add("(min-width: 800px)", () => {
        gsap.to(".circle6", {
          y: -120,
          scrollTrigger: {
            trigger: ".contact",
            start: "top center+=200",
            scrub: 1,
          },
        });
      });
    },
  },
};
</script>

<style>
/* Contact section */
.contact {
  display: flex;
  width: 100%;
  position: relative;
  justify-content: center;
  align-content: center;
}
.bloc-contact {
  width: 70%;
  overflow: hidden;
  z-index: 30;
  margin-bottom: 120px;
  padding-left: 10px;
}
.footer-info {
  font-size: 32px;
  width: 65%;
}
.footer-info span {
  font-weight: 600;
}
.ctn-footer-links {
  display: flex;
  margin-top: 50px;
}
.creator {
  font-size: 13px;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 30px;
  width: 100%;
  border-bottom: var(--linesStyle);
  border-top: var(--linesStyle);
}
#contact .circle-container-footer {
  position: absolute;
  width: 70%;
  left: 15%;
  height: 60vh;
  margin: 0 auto;
  overflow: hidden;
  bottom: 30px;
}

.circle5 {
  width: 200px;
  height: 200px;
  position: absolute;
  bottom: -120px;
  right: 250px;
  background-color: #b2bdfb;
  border-radius: 100%;
}
.circle6 {
  width: 100px;
  height: 100px;
  position: absolute;
  bottom: 140px;
  right: -50px;
  background-color: #ffeeae;
  border-radius: 100%;
}
@media only screen and (max-width: 768px) {
  .bloc-contact {
    width: 80%;
  }
  .footer-info {
    font-size: 32px;
    width: 80%;
  }
}
@media only screen and (max-width: 480px) {
  .bloc-contact {
    width: 100%;
    padding: 0 20px;
    flex-direction: column;
  }
  .footer-info {
    font-size: 18px;
    width: 100%;
    margin-bottom: 45px;
  }
  #contact .circle-container-footer {
    width: 100%;
    left: 0;
  }
  .bloc-contact {
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  .circle6 {
    width: 90px;
    height: 90px;
    bottom: 20px;
    right: -45px;
  }
}
</style>
