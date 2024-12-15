<template>
  <section id="hero">
    <div class="center-bloc">
      <h1 class="fade-in">{{ $t("designerText") }}</h1>
      <h2 class="fade-in second-line">& {{ $t("devText") }}</h2>
      <div class="bloc-description">
        <p class="fade-in description">{{ $t("description") }}</p>
        <div class="loop-elements">
          <div class="semicircle fade-in-left"></div>
          <img
            class="animated-text fade-in-left"
            src="/images/contour.png"
            alt="circular text"
          />
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import gsap from "gsap";
export default {
  name: "HelloWorld",
  components: {},
  mounted() {
    this.heroAnimation();
  },
  methods: {
    heroAnimation() {
      let tl = gsap.timeline();
      tl.to(".fade-in", {
        stagger: 0.15,
        opacity: 1,
        duration: 0.7,
        y: 0,
        ease: "Power1.easeOut",
      })
        .to(".fade-in-left", {
          opacity: 1,
          rotation: 45, // Rotación en grados
          duration: 0.7,
          x: 0,
          ease: "Power1.easeOut",
        })
        .to(".animated-text", {
          opacity: 1,
          rotation: "+=360", // Rotación en grados
          duration: 9, // Duración en segundos
          repeat: -1, // Repetición infinita
          ease: "linear",
        });
    },
  },
};
</script>

<style>
/* Hero section */

#hero {
  display: flex;
  width: 100%;
  min-height: 100vh;
  margin: auto;
  position: relative;
}
.center-bloc {
  margin: 0 auto;
  width: 70%;
  padding: 135px 0 135px 20px;
  display: flex;
  flex-direction: column;
  justify-content: center;
}
h1,
h2,
.second-line,
h3 {
  font-family: "pp_eikothin", sans-serif;
  font-weight: normal;
}
h1,
.second-line {
  font-size: 9vw;
  letter-spacing: -0.02em;
  line-height: 100%;
  margin: 0;
}
.bloc-description {
  width: 100%;
  display: flex;
  position: relative;
  overflow: hidden;
}
.description {
  font-size: 1.15em;
  line-height: 1.5em;
  margin-right: 15px;
  width: 48%;
  margin-top: 40px;
  background-color: #ffeeae;
  padding: 22px 18px;
  border-radius: 40px 40px 40px 0;
}
.loop-elements {
  position: relative;
  width: 50%;
}
.semicircle {
  position: absolute;
  content: "";
  width: 100px;
  height: 100px;
  background-color: var(--pink);
  border-radius: 100%;
  bottom: 50px;
  right: -50px;
}
.fade-in {
  opacity: 0;
  transform: translateY(95px);
}
.fade-in-left {
  opacity: 0;
  transform: translateX(95px);
}
.animated-text {
  width: 200px;
  height: 200px;
  position: absolute;
  bottom: 0px;
  right: -100px;
}

/* End of hero section */

@media screen and (max-width: 1024px) {

  .description {
    width: 60%;
  }
}
@media only screen and (max-width: 768px) {
  .description {
    width: 80%;
    font-size: 1em;
    margin-top: 50px;
  }
  .bloc-description {
    flex-direction: column;
  }
  .center-bloc {
    background-color: transparent;
    width: 80%;
    padding-bottom: 80px;
  }
  .loop-elements {
    position: relative;
    width: 100%;
    height: 30vh;
  }
  h1,
  .second-line {
    font-size: 10vw;
  }
  #all-projects h2 {
    font-size: 80px;
  }
}

@media screen and (max-width: 480px) {
  .center-bloc {
    width: 100%;
    margin: 0;
    padding: 100px 20px 0px;
  }
  .description {
    width: 100%;
  }
  h1,
  .second-line {
    font-size: 14vw;
    line-height: 105%;
  }
  .bloc-description {
    flex-direction: column;
  }
  .semicircle {
    width: 70px;
    height: 70px;
    bottom: 45px;
    right: -35px;
  }
  .animated-text {
    width: 140px;
    height: 140px;
    position: absolute;
    bottom: 10px;
    right: -70px;
  }
}
</style>
