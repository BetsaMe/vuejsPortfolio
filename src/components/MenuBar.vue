<template>
  <div>
    <nav class="nav-desktop">
      <router-link to="/" class="btn-home">
        <p class="logo-mobile">BM</p>
        <p class="logo-desktop">
          Betsabé <br />
          Meneses
        </p>
      </router-link>
      <div class="right-buttons">
        <LocaleSwitcher />
        <a
          class="btn-contact"
          href="mailto: betsamene@gmail.com"
          target="_blank"
          ><span class="underlined-02">CONTACT</span>
        </a>
        <router-link 
          to="/about" 
          class="btn-profile" 
        >
          <span class="underlined-02">{{ $t("buttonProfile") }}</span>
        </router-link>
      </div>

      <div
        class="menu-btn"
        :class="[isOpen ? 'active' : '']"
        @click="toggleMenu()"
      >
        <span class="bar"></span>
        <span class="bar"></span>
      </div>
    </nav>

    <nav class="nav-mobile">
      <router-link to="/" @click="toggleMenu()">
        <span class="btn-open-menu">Home</span>
      </router-link>
      <a
        class="btn-open-menu"
        @click="toggleMenu()"
        href="mailto: betsamene@gmail.com"
        target="_blank"
        ><span>CONTACT</span>
      </a>
      <router-link to="/about" @click="toggleMenu()">
        <span class="btn-open-menu">{{ $t("buttonProfile") }} </span>
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
      isSelect:false
    };
  },
  created() {
    window.addEventListener("scroll", this.showingNavbar);
    window.addEventListener("resize", this.openMenu);
  },
  mounted() {
    gsap.to(".nav-desktop", { opacity: 1, duration: 0.5, ease: "power3.out" });
  },
  unmounted() {
    window.removeEventListener("resize", this.openMenu);
    window.addEventListener("scroll", this.showingNavbar);
  },
  methods: {
    showingNavbar() {
      let navbar = document.querySelector(".nav-desktop");
      if (window.pageYOffset > 0) {
        navbar.classList.add("scrolled");
      } else {
        navbar.classList.remove("scrolled");
      }
    },
    toggleMenu() {
      this.isOpen = !this.isOpen;
      this.openMenu();
    },
    openMenu() {
      if (this.isOpen && window.innerWidth <= 768) {
        gsap.to(".nav-mobile", {
          opacity: 1,
          duration: 0.2,
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
    }
  },
};
</script>

<style scoped>
nav {
  position: fixed;
  top: 0;
  width: 100%;
  transition: 0.2s ease-in-out;
  display: flex;
  justify-content: space-between;
  align-items: center;
  z-index: 30;
  border-bottom: 0.5px solid transparent;
}
nav.scrolled {
  background: var(--white-bg);
  border-bottom: var(--linesStyle);
}
.btn-home {
  width: 15%;
}
.right-buttons {
  display: flex;
  width: 35%;
}
.btn-profile,
.btn-home,
.btn-contact {
  height: 85px;
  display: flex;
  justify-content: center;
  align-items: center;
  transition: all 0.5s ease;
}
.btn-contact,
.btn-profile {
  width: 33%;
}
.btn-home p {
  line-height: 17px;
  font-size: 18px;
  padding: 2px;
  font-weight: 600;
}
.btn-profile span,
.btn-contact span {
  text-transform: uppercase;
  font-size: 15px;
  padding: 5px 8px;
  font-weight: 600;
}
.btn-profile:hover {
  background-size: 100% 2px;
}
.nav-desktop {
  opacity: 0;
}
.logo-mobile {
  display: none;
}

/* burguer menu */
.menu-btn {
  width: 30px;
  height: 30px;
  position: relative;
  overflow: hidden;
  cursor: pointer;
  margin-right: 50px;
  margin-top: 15px;
  display: none;
}
.menu-btn .bar {
  width: 30px;
  height: 2px;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  background-color: var(--grey1);
  transition: all 0.3s ease-in-out;
  z-index: 50;
}
.menu-btn .bar:nth-of-type(1) {
  top: calc(50% - 5px);
}
.menu-btn .bar:nth-of-type(2) {
  top: calc(50% + 5px);
}
.menu-btn.active .bar:nth-of-type(1) {
  top: 50%;
  transform: translate(-50%, 0%) rotate(45deg);
}
.menu-btn.active .bar:nth-of-type(2) {
  top: 50%;
  transform: translate(-50%, 0%) rotate(-45deg);
}
.nav-mobile {
  position: fixed;
  top: 20px;
  right: 20px;
  width: calc(50% - 20px);
  height: 60%;
  padding: 15px;
  background: white;
  border-radius: 5px;
  opacity: 0;
  display: none;
  transition: all 0.7s;
  z-index: 20;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  border: var(--linesStyle);
}
.nav-mobile.active {
  opacity: 1;
}
.btn-open-menu {
  font-size: 25px;
  font-family: "Inter", sans-serif;
  text-transform: uppercase;
  padding: 15px;
}
.languages-mobile {
  margin-top: 18px;
}
@media only screen and (max-width: 768px) {
  .right-buttons {
    display: none;
  }
  .menu-btn {
    display: block;
    z-index: 50;
  }
  .btn-home,
  .btn-contact,
  .btn-profile {
    width: 25%;
    min-width: 115px;
    border: none;
  }
}
@media only screen and (max-width: 480px) {
  
  .btn-home p {
    font-size: 20px;
    color: var(--grey1);
    margin-top: 30px;
  }
  .logo-mobile {
    display: block;    
  }
  .logo-desktop {
    display: none;
  }
  .nav-mobile {
    width: calc(100% - 40px);
    height: 50%;
  }
  .menu-btn {
    margin-right: 40px;
  }
  .btn-open-menu {
    font-size: 18px;
  }
}
</style>
