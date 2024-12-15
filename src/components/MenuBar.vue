<template>
  <div>
    <nav class="nav-desktop">
      <!-- logo -->
      <router-link to="/" class="btn-name">
        <img src="/images/logob.png" alt="logo betsa" class="logo-desktop" />
      </router-link>
      <!-- botones a la derecha -->
      <div class="right-buttons">
        <LocaleSwitcher />
        <router-link to="/about" class="btn-secondary">
          <span class="underlined-02">{{ $t("buttonProfile") }}</span>
        </router-link>
        <router-link to="/contact" class="btn-secondary">
          <span class="underlined-02">{{ $t("buttonContact") }}</span>
        </router-link>
      </div>
      <!-- menu hamburguesa -->
      <div class="btn-burguer-ctn">
        <div
          class="btn-burguer"
          :class="[isOpen ? 'active' : '']"
          @click="toggleMenu()"
        >
          <span class="bar"></span>
          <span class="bar"></span>
        </div>
      </div>
    </nav>

    <!-- menu movil abierto -->
    <nav class="nav-mobile">
      <router-link to="/" @click="toggleMenu()" class="btn-nav-mobile">
        Home
      </router-link>
      <router-link to="/about" @click="toggleMenu()" class="btn-nav-mobile">
        {{ $t("buttonProfile") }}
      </router-link>
      <router-link to="/contact" class="btn-nav-mobile" @click="toggleMenu()">
        CONTACT
      </router-link>
      <LocaleSwitcher class="languages-mobile" />
    </nav>
  </div>
</template>

<script>
import gsap from "gsap";
import LocaleSwitcher from "./LocaleSwitcher.vue";

export default {
  name: "MenuBar",
  components: { LocaleSwitcher },
  data() {
    return {
      isOpen: false,
      isSelect: false,
    };
  },
  created() {
    window.addEventListener("scroll", this.showingNavbar);
    window.addEventListener("resize", this.handleResize);
  },

  mounted() {
    gsap.to(".nav-desktop", { opacity: 1, duration: 0.5, ease: "power3.out" });
  },
  beforeUnmount() {
    window.removeEventListener("scroll", this.showingNavbar);
    window.removeEventListener("resize", this.handleResize);
  },
  methods: {
    showingNavbar() {
      let navbar = document.querySelector(".nav-desktop");

      window.addEventListener("scroll", function () {
        if (window.scrollY > 0) {
          navbar.classList.add("scrolled");
        } else {
          navbar.classList.remove("scrolled");
        }
      });
    },
    toggleMenu() {
      this.isOpen = !this.isOpen;
      this.handleResize();
    },
    handleResize() {
      if (this.isOpen && window.innerWidth <= 768) {
        gsap.to(".nav-mobile", {
          opacity: 1,
          duration: 0.1,
          ease: "power3.out",
        });
        gsap.to(".nav-mobile", { display: "flex" });
      } else {
        gsap.to(".nav-mobile", {
          opacity: 0,
          duration: 0.05,
          ease: "power3.out",
        });
        gsap.to(".nav-mobile", { display: "none" });
      }
    },
  },
};
</script>

<style scoped>
nav {
  position: fixed;
  top: 0;
  width: 100%;
  display: flex;
  justify-content: space-between;
  align-items: center;
  z-index: 20;
  height: 85px;
  border-bottom: 0.5px solid transparent;
  padding: 0 60px;
  transition: background-color 0.2s ease-in-out, border-bottom 0.2s ease-in-out;
}
nav.scrolled {
  background: var(--white-bg);
  border-bottom: var(--linesStyle);
}
.nav-desktop {
  opacity: 0;
  transition: opacity 0.5s ease;
}
.right-buttons {
  display: flex;
}
.btn-secondary,
.btn-name {
  display: flex;
  justify-content: center;
  align-items: center;
  transition: all 0.5s ease;
}
.btn-secondary {
  width: 120px;
  height: 47px;
  margin-left: 40px;
}
.btn-secondary span {
  text-transform: uppercase;
  font-size: 15px;
  padding: 5px 0px;
  font-weight: 600;
}
.btn-secondary:hover {
  background-size: 100% 3px;
}

.logo-desktop {
  height: 38px;
}
/* burguer menu */
.btn-burguer-ctn {
  /* position: fixed;
  top: 35px;
  right:40px;   */
  display: none; 
  z-index: 50;
}
.btn-burguer {
  width: 30px;
  height: 30px;
  position: relative;
  overflow: hidden;
  cursor: pointer;
}
.btn-burguer .bar {
  width: 30px;
  height: 2.5px;
  border-radius: 10px;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  background-color: var(--grey1);
  transition: all 0.3s ease-in-out;
  z-index: 500;
}

.btn-burguer .bar:nth-of-type(1) {
  top: calc(50% - 5px);
}
.btn-burguer .bar:nth-of-type(2) {
  top: calc(50% + 5px);
}
.btn-burguer.active .bar:nth-of-type(1) {
  top: 50%;
  transform: translate(-50%, 0%) rotate(45deg);
}
.btn-burguer.active .bar:nth-of-type(2) {
  top: 50%;
  transform: translate(-50%, 0%) rotate(-45deg);
}
.nav-mobile {
  position: fixed;
  top: 10px;
  right: 10px;
  width: calc(50% - 20px);
  height: 60%;
  padding: 15px;
  background: #FFEEAE;
  border-radius: 20px 0 20px 20px;
  opacity: 0;
  display: none;
  transition: all 0.7s;
  z-index: 15;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  border: var(--linesStyle);
}
.nav-mobile.active {
  opacity: 1;
}
.btn-nav-mobile {
  font-size: 32px;
  font-family: "Inter", sans-serif;
  text-transform: uppercase;
  margin-bottom: 10px;
}
.languages-mobile {
  margin-top: 15px;
}
/* underline effect */
.underlined-02 {
  background-image: linear-gradient(180deg, var(--pink), var(--pink));
  background-repeat: no-repeat;
  background-position: 0 100%;
  transition: background-size 0.3s ease;
  background-size: 0 2px;
}
.underlined-02:hover {
  background-size: 100% 2px;
}
@media only screen and (max-width: 768px) {
  .nav-desktop{
    padding: 0 20px;
  }
  .right-buttons {
    display: none;
  }
  .btn-burguer-ctn {
    display: block;
    z-index: 50;
  }
}
@media only screen and (max-width: 480px) { 
  .nav-mobile {
    width: calc(100% - 20px);
    height: 50%;
  }
  .btn-nav-mobile {
    font-size: 28px;
  }
}
</style>
