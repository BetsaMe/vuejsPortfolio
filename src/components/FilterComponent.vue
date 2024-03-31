<template>
  <div class="project-selection">
    <h3 class="scroll-fade">{{ $t("projectTitle") }}</h3>
    <ul>
      <li class="btn-filter scroll-fade" @click="btnClickHandler">
        <span class="arrow" :class="typeOfProject ? 'arrow-visible' : ''">
        </span>
        <span
          class="text underlined-02"
          :class="typeOfProject ? 'selected-tab' : ''"
          >UI/UX Design</span
        >
      </li>
      <li class="btn-filter scroll-fade" @click="btnClickHandler">
        <span class="arrow" :class="!typeOfProject ? 'arrow-visible' : ''">
        </span>
        <span
          class="text underlined-02"
          :class="!typeOfProject ? 'selected-tab' : ''"
          >{{ $t("filtertext") }}</span
        >
      </li>
    </ul>
  </div>
</template>

<script>
import gsap from "gsap";
import ScrollTrigger from "gsap/ScrollTrigger";
export default {
  name: "FilterComponent",
  props: {
    btnClickHandler: { type: Function },
    typeOfProject: { type: Boolean },
  },
  mounted() {
    ScrollTrigger.refresh();
    gsap.registerPlugin(ScrollTrigger);
    this.revealText();
  },
  methods: {
    revealText() {
      let el = gsap.utils.toArray(".scroll-fade");
      el.forEach((element) => {
        gsap.from(element, {
          scrollTrigger: { trigger: element },
          duration: 0.7,
          ease: "power2",
          y: 60,
          opacity: 1,
          stagger: 0.9,
        });
      });
    },
  },
};
</script>

<style>
/* Project filters */
.project-selection {
  display: flex;
  align-items: flex-end;
  justify-content: space-between;
  margin: 0 15% 50px;
  padding: 30px 40px;
}

.project-selection h3 {
  font-size: 7.5vw;
  margin: 0;
  line-height: 100%;
  width: 50%;
}
.project-selection ul {  
  padding: 0;
  margin: 0;
  z-index: 14;
  display: flex;
  flex-direction: column;
  align-items: flex-end;
  width: 50%;
}
.btn-filter {
  position: relative;
  padding: 10px 10px 0;
  text-decoration: none;
  text-transform: uppercase;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: flex-end;
}
.btn-filter .text {
  font-weight: 500;
  font-size: 18px;
  width: max-content;
  padding: 5px 0;
}
.arrow {
  content: url("/public/images/arrow-right.svg");
  height: 28px;
  width: 28px;
  transition: transform 0.5s cubic-bezier(0.86, 0, 0.07, 1),
    opacity 0.4s cubic-bezier(0.86, 0, 0.07, 1);
  display: inline-block;
  margin-right: 10px;
  transform-origin: left center;
  opacity: 0;
  transform: translateX(-75%) scaleX(0.1);
}
.arrow-visible {
  opacity: 1;
  transform: translateX(0) scaleX(1);
}
.btn-filter .selected-tab {
  font-weight: 600;
  background-position: 100% 100%;
  background-size: 50% 2px;
}
@media only screen and (max-width: 1024px) {
  .project-selection {
    padding: 30px;
  }
  .project-selection h3 {
    font-size: 80px;
  }
}
@media only screen and (max-width: 768px) {
  .project-selection {
    margin: 0 10% 50px;
  }
  .project-selection h3 {
    font-size: 60px;
  }
  .btn-filter {
    padding: 4px 10px 0;
  }
  .btn-filter .text {
    font-size: 14px;
  }
}
@media screen and (max-width: 480px) {
  .project-selection {
    flex-direction: column;
    align-items: flex-start;
    margin: 0;
  }
  .project-selection h3 {
    font-size: 65px;
    margin-bottom: 10px;
  }
  .project-selection ul {
    flex-direction: row;
    justify-content: space-evenly;
    margin: 10px 0;
    width: 100%;
  }
  .btn-filter {
    padding: 0;
  }
  .arrow {
    display: none;
  }
  .text {
    margin: 0;
    padding: 4px;
  }
}
</style>
