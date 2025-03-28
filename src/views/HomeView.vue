<template>
  <HeroSection />
  <section id="all-projects">
    <div class="project-selection">
      <h3 class="scroll-fade">{{ $t("projectTitle") }}</h3>
      <FilterComponent :isDesign="isDesign" @changeCategory="toggleCategory" />
    </div>

    <transition-group name="list" @before-enter="beforeEnter" @enter="enter">
      <div :id="projet.id" v-for="projet in projetCategory" :key="projet.id">
        <div class="project-content-container">
          <div class="project-text">
            <div class="ctn-number scroll-content">
              <span class="big-number"> {{ projet.number }} </span>
            </div>
            <div class="project-description">
              <h4 class="scroll-content">{{ projet.name }}</h4>
              
              <ul class="tech-label-container scroll-content">
                <li
                  class="tech-label"
                  v-for="element in projet.tags"
                  :key="element"
                >
                  <div class="little-dot"></div>
                  {{ element }}
                </li>
              </ul>
              <p class="scroll-content">{{ $t(projet.homeText) }}</p>
              <router-link
                :to="{ name: 'single', params: { slug: projet.slug } }"
              >
                
                <ArrowBtn :title="$t(('button01'))" class="scroll-content" />
              </router-link>
            </div>
          </div>
          <router-link
            class="img-container"
            :to="{ name: 'single', params: { slug: projet.slug } }"

          >
            <div class="sub-container">
              <img
                class="projet-img"
                :src="projet.coverImage"
                :alt="projet.alt"
              />
            </div>
          </router-link>
        </div>
      </div>
    </transition-group>
  </section>
</template>

<script>
import HeroSection from "@/components/HeroSection.vue";
import gsap from "gsap";
import ScrollTrigger from "gsap/ScrollTrigger";
import data from "../data";
import FilterComponent from "@/components/FilterComponent.vue";
import ArrowBtn from "@/components/ArrowBtn.vue";

export default {
  name: "HomeView",
  components: {
    HeroSection,
    FilterComponent,
    ArrowBtn,
  },
  data() {
    return {
      projets: data,
      isDesign: true,
      mm: gsap.matchMedia(), // Instancia globalmente
    };
  },
  computed: {
    projetCategory() {
      const category = this.isDesign ? "design" : "code";
      return this.projets.filter((projet) => projet.category === category);
    },
    projectSlug() {
      return this.$route.params.slug;
    },
  },

  mounted() {
    ScrollTrigger.refresh();
    gsap.registerPlugin(ScrollTrigger);
    this.initGSAPAnimations();
    window.addEventListener("resize", this.refreshScrollTrigger);
  },
  unmounted() {
    window.removeEventListener("resize", this.refreshScrollTrigger);
  },
  methods: {
    refreshScrollTrigger() {
      ScrollTrigger.refresh();
    },
    beforeEnter(el) {
      el.style.opacity = 0;
    },
    enter(el, done) {
      gsap.to(el, { duration: 2, opacity: 1, onComplete: done });
    },
    initGSAPAnimations() {
      this.revealImages();
      this.revealContent();
    },
    toggleCategory(value) {
      this.isDesign = value;
    },
    revealImages() {
      this.mm.add("(min-width: 800px)", () => {
        let images = gsap.utils.toArray(".img-container");
        images.forEach((image) => {
          gsap.fromTo(
            image,
            { opacity: 0 },
            {
              opacity: 1,
              duration: 0.5,
              scrollTrigger: {
                trigger: image,
                start: "top center",
                // scrub: 1,
              },
            }
          );
        });
        // Limpieza de GSAP cuando el matchMedia deja de aplicar
        return () =>
          images.forEach((image) => ScrollTrigger.killTweensOf(image));
      });
    },
    revealContent() {
      this.$nextTick(() => {
        this.mm.add("(min-width: 800px)", () => {
          let el = gsap.utils.toArray(".scroll-content");
          el.forEach((element) => {
            gsap.from(element, {
              scrollTrigger: { trigger: element },
              duration: 0.7,
              ease: "power2",
              y: 100,
              opacity: 1,
              stagger: 0.7,
            });
            return () => ScrollTrigger.getAll().forEach((t) => t.kill());
          });
        });
      });
    },
  },
};
</script>

<style>
.project-content-container {
  display: grid;
  grid-template-columns: 15% 35% 35% 15%;
  grid-template-rows: 450px 100px;
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
  font-family: "pp_eikothin", sans-serif;
  font-weight: normal;
  left: -50px;
}
.project-description {
  padding: 20px 5px;
  font-size: 16px;
  line-height: 28px;
}
.project-description h4 {
  margin: 0 0 15px;
  font-size: 54px;
  line-height: 42px;
  font-family: "pp_eikothin", sans-serif;
  font-weight: normal;
}
.project-description p {
  margin: 20px 0 60px;
}
/* Projet labels */
.tech-label-container {
  margin: 10px 0;
  display: flex;
  flex-wrap: wrap;
  justify-content: flex-start;
  padding: 0;
}
.little-dot {
  width: 5px;
  height: 5px;
  background-color: var(--purple);
  border-radius: 5px;
  margin-right: 5px;
}
.tech-label {
  font-size: 0.9em;
  font-weight: 500;
  text-align: center;
  margin: 0 10px 0 0;
  list-style: none;
  display: flex;
  align-items: center;
}
.img-container {
  grid-column: 3/4;
  grid-row: 1/2;
  display: flex;
  align-items: center;
  justify-content: center;
}
.sub-container {
  height: 100%;
  width: 100%;
  overflow: hidden;
}
.projet-img {
  position: relative;
  object-fit: cover;
  height: 100%;
  width: 100%;
  transition: transform 0.3s; /* Para navegadores modernos */
  -webkit-transition: -webkit-transform 0.3s; /* Para navegadores antiguos */
  cursor: url("/public/images/black-circle.svg"), auto;
}
.projet-img:hover {
  transform: scale(1.1, 1.1);
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
  .circle2 {
    right: -250px;
  }
}
@media only screen and (max-width: 768px) {
  .project-content-container {
    grid-template-columns: 10% 1fr 10%;
    grid-template-rows: 350px 1fr 80px;
  }
  .big-number {
    font-size: 140px;
    left: -5%;
  }
  .project-description {
    padding: 20px;
  }
  .projet-img {
    padding: 10px;
  }
  .projet-img:hover {
    height: 100%;
    width: 100%;
  }
  .img-container {
    padding: 0;
  }
}

@media screen and (max-width: 480px) {
  .project-text,
  .img-container {
    grid-column: 1/-1;
  }
  .project-content-container {
    grid-template-columns: 1fr;
    grid-template-rows: 300px 1fr 50px;
  }
  .ctn-number {
    display: none;
  }
  .img-container {
    opacity: 1;
  }
  .project-description h4 {
    font-size: 36px;
    margin-bottom: 10px;
  }
  .project-selection {
    padding: 0 20px;
  }
  .project-selection ul {
    justify-content: space-between;
  }
  .tech-label{
    font-size: 14px;
  }
  .projet-img {
    padding: 0px;
  }
  .project-description p{
    margin: 15px 0 30px;
  }
  .projet-img:hover {
    transform: none;
  }
}
</style>
