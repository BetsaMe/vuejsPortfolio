<template>
  <section class="about">
    <div class="center-bloc-about">
      <div class="about-text">
        <h4>{{ $t("about") }}</h4>
        <div class="bloc-1">
          <div class="bloc-1-txt">
            <p class="anim-2">{{ $t("aboutP1") }}</p>
            <p class="anim-2">{{ $t("aboutP2") }}</p>
            <p class="anim-2">{{ $t("aboutP3") }}</p>
            <p class="anim-2">{{ $t("aboutP4") }}</p>
          </div>
          <div class="bloc-1-img">
            <img src="images/life01.png" alt="pictures" class="anim-2" />
            <div class="shape-01"></div>
          </div>
        </div>
        <div class="bloc-2">
          <div class="bloc-2-img">
            <img src="images/life02.png" alt="pictures" class="anim-2" />
            <div class="shape-02"></div>
          </div>
          <div class="bloc-2-txt">
            <p class="anim-2">{{ $t("aboutP5") }}</p>
            <p class="anim-2">{{ $t("aboutP6") }}</p>
          </div>
        </div>
        <a href=""></a>

        <a
          href="images/CV-Betsa-Meneses.pdf"
          download="CV-Betsa"
          class="ctn-btn-download anim-2"
        >
          <DownloadBtn
            :title="'download'"
            :bgColor="'#fff'"
            :textColor="'#616fe4'"
            :borderColor="'#616fe4'"
            :hoverBgColor="'#616fe4'"
            :hoverTextColor="'#fff'"
            :hoverBorderColor="'#616fe4'"
          />
        </a>
      </div>
    </div>
  </section>
</template>

<script>
import gsap from "gsap";
import ScrollTrigger from "gsap/ScrollTrigger";
import DownloadBtn from "@/components/DownloadBtn.vue";
export default {
  name: "AboutView",
  components: {
    DownloadBtn,
  },
  mounted() {
    gsap.registerPlugin(ScrollTrigger);
    this.aboutAnimation();
    this.parallaxShapes();
  },
  methods: {
    aboutAnimation() {
      let tl = gsap.timeline();
      tl.to(".anim-2", {
        stagger: 0.1,
        opacity: 1,
        duration: 1,
        y: 0,
        ease: "power2.inOut",
      });
    },
    parallaxShapes() {
      let mm = gsap.matchMedia();
      mm.add("(min-width: 800px)", () => {
        gsap.to(".shape-01", {
          y: -120,
          scrollTrigger: {
            trigger: ".bloc-1-txt",
            start: "top center+=200",
            scrub: 2,
          },
        });

        gsap.to(".shape-02", {
          y: -120,
          scrollTrigger: {
            trigger: ".bloc-2",
            start: "top center+=200",
            scrub: 2,
          },
        });
      });
    },
  },
};
</script>

<style>
.anim-2 {
  opacity: 0;
  transform: translateY(40px);
}
.about {
  position: relative;
  z-index: 14;
  min-height: 100vh;
}

/* About section */
.center-bloc-about {
  width: 70%;
  margin: 0 15% 40px;
  padding: 125px 0 50px;
}
.center-bloc-about h4 {
  padding: 0 20px;
}
.bloc-1,
.bloc-2 {
  width: 100%;
  display: flex;
  justify-content: space-between;
  padding: 0 20px;
}
.bloc-1 {
  margin-bottom: 50px;
}
.bloc-1-txt,
.bloc-2-txt {
  width: 50%;
  font-size: 17px;
  line-height: 24px;
}
.bloc-1-img,
.bloc-2-img {
  width: 50%;
  position: relative;
}
.bloc-1-img img,
.bloc-2-img img {
  width: 100%;
}
.about-text > h4 {
  font-family: "pp_eikothin", sans-serif;
  font-weight: 200;
  font-size: 5vw;
  line-height: 100%;
  margin: 20px 0 30px;
}
.shape-01,
.shape-02 {
  width: 140px;
  height: 140px;
  border-radius: 50%;
  position: absolute;
  z-index: -2;
}
.shape-01 {
  top: 50%;
  right: 40%;
  background-color: #b2bdfb;
}
.shape-02 {
  top: 50%;
  right: 40%;
  border-radius: 0 50% 50% 0;
  background-color: #ffeeae;
}
.ctn-btn-download {
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  margin-top: 25px;
}

@media only screen and (max-width: 1024px) {
  .bloc-1,
  .bloc-2 {
    padding: 0 20px;
  }
  .about-text > h4 {
    font-size: 8vw;
  }
}
@media screen and (max-width: 768px) {
  .bloc-1,
  .bloc-2 {
    flex-direction: column;
    width: 100%;
  }
  .bloc-1-txt,
  .bloc-2-txt {
    width: 100%;
  }
  .bloc-1-img {
    width: 100%;
    margin: 0 auto;
  }
  .bloc-2-img {
    display: none;
  }
}
@media screen and (max-width: 480px) {
  .center-bloc-about {
    width: 100%;
    margin: 0;
    padding: 75px 0;
  }
  .bloc-1,
  .bloc-2 {
    padding: 0 20px;
  }
  .about-text > h4 {
    font-size: 12vw;
    padding: 0 10px;
  }
}
</style>
