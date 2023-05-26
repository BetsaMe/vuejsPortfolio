<template>
  <section id="hero">
    <div class="center-bloc">
      <p class="hello fade-in">Hello! {{ $t("hello") }}</p>
      <h1 class="fade-in">{{ $t("designerText") }}</h1>
      <h2 class="fade-in second-line">& {{ $t("devText") }}</h2>
      <p class="fade-in description">{{ $t("description") }}<span>🎨👩🏽‍💻✨💫</span></p>
    </div>
  </section>
</template>

<script>
import gsap from "gsap";
export default {
  name: "HelloWorld",
  mounted() {
    this.heroAnimation();
  },
  methods: {
    heroAnimation() {
      let tl = gsap.timeline();      
      tl.to(".fade-in", {
        stagger: 0.15,
        opacity: 1,
        duration: 1,
        y: 0,
        ease: "Power1.easeOut"
      })
      .to(".circle1, .circle2", {
        stagger: 0.15,
        opacity: 0.6,
        duration: 0.7,
        ease: "Power1.easeOut"
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
  margin: 0 15%;
  width: 70%;
  padding: 135px 40px;
  display: flex;
  flex-direction: column;
  justify-content: center;
}
.hello {
  font-size: 1.1em;
  margin-bottom: 15px;
}
h1,
h2,
.second-line,
h3 {
  font-family: 'Inter', sans-serif;
  font-weight: 200;
}
h1,
.second-line {
  font-size: 8vw;
  letter-spacing: -0.02em;
  line-height: 100%;
  margin: 0;
}
.description {
  font-size: 1.15em;
  line-height: 1.5em;
  margin-right: 15px;
  width: 47%;
  margin-top: 40px;
}
.fade-in {
  opacity: 0;
  transform: translateY(65px);
}
/* End of hero section */

@media screen and (max-width: 1024px) {
  .center-bloc {
    padding: 85px 30px 0;
  }
}
@media only screen and (max-width: 768px) {
  .description {
    width: 100%;
    margin: 30px 0;
  }
  .center-bloc {
    margin: 0 10%;
    width: 80%;
    background-color: transparent;
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
    padding: 100px 20px 60px;
  }
  .description {
    font-size: 1.1em;
    text-align: start;
    padding-left: 5px;
  }
  .hello {
    font-size: 1.1em;
    margin-bottom: 18px;
    padding-left: 5px;
  }
  h1,
  .second-line {
    font-size: 14vw;
    line-height: 105%;
  }
}
</style>
