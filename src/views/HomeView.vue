<template>
  <div class="circle-container">
    <div class="circle1"></div>
    <div class="circle2"></div>
  </div>
  <HeroSection />
  <section id="all-projects">
    <FilterComponent
      :btnClickHandler="this.toggleCategory"
      :typeOfProject="this.isDesign"
    />

    <div class="project-content">
      <transition-group
        name="list"
        mode="in-out"
        @before-enter="beforeEnter"
        @enter="enter"
      >
        <div :id="projet.id" v-for="projet in projetCategory" :key="projet.id">
          <div class="project-content-container">
            <div class="project-text">
              <div class="ctn-number scroll-content">
                <span class="big-number"> {{ projet.number }} </span>
              </div>
              <div class="project-description">
                <h4 class="scroll-content">{{ projet.title }}</h4>
                <p class="scroll-content">{{ $t(projet.homeText) }}</p>
                <ul class="tech-label-container scroll-content">
                  <li
                    class="tech-label"
                    v-for="element in projet.techno"
                    :key="element"
                  >
                    {{ element }}
                  </li>
                </ul>
                <router-link
                  :to="'work'+ { name: 'single', params: { projetId: projet.id } }"
                  class="btn-arrow underlined-02 scroll-content"
                >
                  <span>decouvrir</span>
                  <img src="/images/arrow-01.svg" alt="arrow" />
                </router-link>
              </div>
            </div>
            <router-link
              class="img-container"
              :to="{ name: 'single', params: { projetId: projet.id } }"
            >
              <img
                class="projet-img"
                :src="projet.coverImage"
                :alt="projet.alt"
              />
            </router-link>
          </div>
        </div>
      </transition-group>
    </div>
  </section>
</template>

<script>
import HeroSection from "@/components/HeroSection.vue";
import gsap from "gsap";
import ScrollTrigger from "gsap/ScrollTrigger";
import data from "../data";
import FilterComponent from "@/components/FilterComponent.vue";

export default {
  name: "HomeView",
  components: {
    HeroSection,
    FilterComponent,
  },
  data() {
    return {
      projets: data,
      isDesign: true,
    };
  },
  computed: {
    projetCategory: function () {
      if (this.isDesign) {
        return this.projets.filter((projet) => projet.category === "design");
      } else {
        return this.projets.filter((projet) => projet.category === "code");
      }
    },
  },
  mounted() {
    ScrollTrigger.refresh();
    gsap.registerPlugin(ScrollTrigger);
    this.revealImages();
    this.revealContent();
    window.addEventListener("resize", ScrollTrigger.refresh());
  },
  unmounted() {
    window.removeEventListener("resize", ScrollTrigger.refresh());
  },
  setup() {
    const beforeEnter = (el) => {
      el.style.opacity = 0;
    };
    const enter = (el, done) => {
      gsap.to(el, {
        duration: 2,
        opacity: 1,
        onComplete: done,
      });
    };
    return { beforeEnter, enter };
  },
  methods: {
    toggleCategory() {
      this.isDesign = !this.isDesign;
    },
    revealImages() { 
      let mm = gsap.matchMedia();
      mm.add("(min-width: 800px)", () =>{
        let images = gsap.utils.toArray(".img-container");
          images.forEach((image) => {
            gsap.fromTo(image,{opacity: 0}, {
              opacity: 1,
              duration: 0.5,
              scrollTrigger: {
                trigger: image,
                start: "top center",
                // scrub: 1,
              },
            });
          });
      })
    },
    revealContent() {
      this.$nextTick(() =>{
        let mm = gsap.matchMedia();
        mm.add("(min-width: 800px)", () =>{
          let el = gsap.utils.toArray(".scroll-content");
            el.forEach((element) => {
              gsap.from(element, {
                scrollTrigger: { trigger: element },
                duration: 0.7,
                ease: "power2",
                y: 70,
                opacity: 1,
                stagger: 0.9,
              });
            });
        });
      })
    },
  },
};
</script>

<style>
.project-content {
  margin: 0;
}
.project-content-container {
  display: grid;
  grid-template-columns: 15% 35% 35% 15%;
  grid-template-rows: 1fr 100px;
  transition: 1s ease all;
}
/* Dont delete this */
.project-text {
  grid-column: 2/3;
  grid-row: 1/2;
  position: relative;
}
.ctn-number {
  overflow: hidden;
  display: flex;
  align-items: flex-end;
  margin: 0;
  padding: 0;
}
.big-number {
  position: relative;
  font-size: 170px;
  line-height: 170px;
  font-family: "Inter", sans-serif;
  font-weight: 200;
  left: -60px;
}
.project-description {
  padding: 20px 50px;
  font-size: 17px;
  line-height: 28px;
}
.project-description h4 {
  margin: 0;
  font-size: 26px;
  text-transform: uppercase;
}
/* Projet labels */
.tech-label-container {
  margin: 10px 0;
  display: flex;
  flex-wrap: wrap;
  justify-content: flex-start;
  padding: 0;
}
.tech-label {
  font-size: 0.9em;
  font-weight: 500;
  text-align: center;
  margin: 0 8px 0 0;
  list-style: none;
}
.tech-label::after {
  content: "»";
  display: inline-block;
  color: var(--grey1);
  margin-left: 3px;
}
.btn-arrow {
  display: flex;
  align-items: center;
  width: fit-content;
}
.btn-arrow span {
  text-transform: uppercase;
  font-size: 14px;
  font-weight: 600;
  margin-right: 8px;
}
.btn-arrow img {
  height: 30px;
  width: 30px;
}
.btn-arrow:hover {
  background-size: 100% 2px;
}
.img-container {
  grid-column: 3/4;
  grid-row: 1/2;
}
.projet-img {
  position: relative;
  object-fit: cover;
  height: 100%;
  width: calc(100% - 11px);
  left: 10px;
  cursor: url("/public/images/arrow-02.png"), auto;
}
/* Gradients */
.circle-container {
  position: absolute;
  width: 100%;
  height: 100%;
  overflow: hidden;
}
.circle1,
.circle2 {
  position: absolute;
  content: "";
  opacity: 0;
}
.circle1 {
  width: 300px;
  height: 380px;
  top: -110px;
  left: -30px;
  background: radial-gradient(190px, #c5c6ff, transparent);
  filter: blur(20px);
}
.circle2 {
  width: 500px;
  height: 500px;
  top: 50vh;
  right: -110px;
  background: radial-gradient(280px, #96f5e8, transparent);
  filter: blur(60px);
}

/* End Animated gradients */
@media only screen and (max-width: 1024px) {
  .project-content-container {
    grid-template-columns: 15% 1fr 15%;
    grid-template-rows: 1fr auto 80px;
  }
  .project-text,
  .img-container {
    grid-column: 2/3;
  }
  .project-text {
    grid-row: 2/3;
  }
  .projet-img {
    width: calc(100% - 1px);
    left: 0;
  }
  .circle2 {
    right: -250px;
  }
}
@media only screen and (max-width: 768px) {
  .project-content-container {
    grid-template-columns: 10% 1fr 10%;
    grid-template-rows: 350px 1fr;
  }
  .big-number {
    font-size: 140px;
    left: -5%;
  }
  .project-description {
    padding: 20px;
  }
  .img-container {
    height: 350px;
  }
}

@media screen and (max-width: 480px) {
  .project-text,
  .img-container {
    grid-column: 1/-1;
  }

  .project-content-container {
    grid-template-columns: 1fr;
    grid-template-rows: 300px 1fr;
  }
  .ctn-number {
    display: none;
  }
  .img-container {
    height: 300px;
    border: none;
    border-bottom: var(--linesStyle);
  }
  .btn-arrow span {
    font-size: 12px;
  }
  .project-description {
    margin: 20px 0 10px;
  }
  .project-description h4 {
    font-size: 20px;
  }
  .project-description p {
    margin: 16px 0 0;
  }
  .circle1 {
    display: none;
  }
  .circle2 {
    top: 55vh;
    width: 300px;
    height: 300px;
    background: radial-gradient(150px, #96f5e8, transparent);
    right: -140px;
  }
}
</style>
