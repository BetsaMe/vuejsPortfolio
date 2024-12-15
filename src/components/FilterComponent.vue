<template>
  <div class="project-selection">
    <h3 class="scroll-fade">{{ $t("projectTitle") }}</h3>
    <ul class="scroll-fade">
      <li
        v-for="(item, index) in [
          { text: 'UI/UX Design', type: true },
          { text: $t('filtertext'), type: false },
        ]"
        :key="index"
        class="btn-filter"
        @click="selectTab(index)"
        :class="selectedIndex === index ? 'selected-tab' : ''"
      >
        <div class="ctn-arrow" v-if="selectedIndex === index">
          <span class="arrow"></span>
        </div>
        <span class="text">{{ item.text }}</span>
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
  data() {
    return {
      selectedIndex: 0, // Almacena el índice del botón seleccionado
    };
  },
  mounted() {
    ScrollTrigger.refresh();
    gsap.registerPlugin(ScrollTrigger);
    this.revealText();
  },
  methods: {
    selectTab(index) {
      if (this.selectedIndex !== index) {
        this.selectedIndex = index;
        this.btnClickHandler(index); // Pasa el índice seleccionado al padre
      }
    },
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
  flex-direction: column;
  margin: 0 15%;
  padding: 30px 20px;
}

.project-selection h3 {
  font-size: 7.5vw;
  margin: 0;
  line-height: 100%;
  width: 100%;
}
.project-selection ul {
  padding: 0;
  margin: 50px 0;
  z-index: 14;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
}
.btn-filter {
  position: relative;
  text-decoration: none;
  text-transform: uppercase;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  width: 220px;
  height: 45px;
  background-color: #fff;
  border: 1px solid #616fe4;
  margin: 0 20px;
  border-radius: 60px;
  transition: all 0.3s cubic-bezier(0.86, 0, 0.07, 1);
}
.btn-filter:hover {
  background-color: #616fe4;
  color: #fff;
}
.btn-filter .text {
  font-weight: normal;
  font-size: 16px;
  width: max-content;
}
/* Arrow container */
.ctn-arrow {
  position: relative;
  display: inline-block;
  overflow: hidden;
  width: 28px;
  height: 28px;
}
.arrow {
  position: absolute;
  top: 0;
  left: 0;
  content: url("/public/images/whitearrow-01.svg");
  height: 28px;
  width: 28px;
  transition: transform 0.3s cubic-bezier(0.86, 0, 0.07, 1);
  transform-origin: left center;
  opacity: 1;
}
.selected-tab {
  font-weight: 600;
  background-color: #616fe4;
  color: #fff;
}

/* Responsive Styles */
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
    margin: 0 10%;
    padding-bottom: 0;
  }
  .project-selection h3 {
    font-size: 60px;
  }
  .btn-filter {
    min-width: 160px;
  }
  .btn-filter .text {
    font-size: 14px;
  }
}
@media screen and (max-width: 480px) {
  .project-selection {
    margin: 30px 0;
  }
  .project-selection h3 {
    font-size: 65px;
    margin-bottom: 10px;
    width: 100%;
  }
  .project-selection ul {
    margin: 25px 0;
    flex-direction: column;
  }
  .project-selection ul li {
    margin: 10px;
  }
  .btn-filter {
    height: 44px;
    width: auto;
  }
  .btn-filter .text {
    font-size: 12px;
  }
}
</style>
