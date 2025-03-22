<template>
  <ul class="category-tabs scroll-fade">
    <li
      class="btn-filter"
      :class="{ 'selected-tab-purple': isDesign }"
      @click="$emit('changeCategory', true)"
    >
      <div class="ctn-arrow" v-if="isDesign">
        <img
          :src="'/images/whitearrow-01.svg'"
          class="arrow"
          alt="arrow"
        />
      </div>
      <span class="text">UI/UX Design</span>
    </li>
    <li
      class="btn-filter"
      :class="{ 'selected-tab-yellow': !isDesign }"
      @click="$emit('changeCategory', false)"
    >
      <div class="ctn-arrow" v-if="!isDesign">
        <img
          :src="'/images/whitearrow-01.svg'"
          class="arrow"
          alt="arrow"
        />
      </div>
      <span class="text">Desarrollo web</span>
    </li>
  </ul>
</template>

<script>
import gsap from "gsap";
import ScrollTrigger from "gsap/ScrollTrigger";
export default {
  name: "FilterComponent",
  props: {
    isDesign: { type: Boolean },
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
  margin: 0 20px;
  border-radius: 60px;
  transition: all 0.3s cubic-bezier(0.86, 0, 0.07, 1);
}
.btn-filter{
  background-color: #fff;
  border: 1px solid var(--purple);
}
.btn-filter:hover{
  background-color: #B2BDFB;
  color: var(--grey2);
}
.selected-tab-yellow, .selected-tab-purple{
  background-color: var(--purple);
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
  height: 28px;
  width: 28px;
  transition: transform 0.3s cubic-bezier(0.86, 0, 0.07, 1);
  transform-origin: left center;
  opacity: 1;
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
    min-width: 140px;
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
    padding: 0 10px;
  }
  .project-selection ul {
    margin: 25px 0;
    justify-content:space-around;
  }
  .project-selection ul li {
    margin: 4px;
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
