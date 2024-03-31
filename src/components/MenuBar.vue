<template>
  <div>
    <nav class="nav-desktop">
      <router-link to="/" class="btn-name">
        <span class="logo-mobile">BM</span>
        <span class="logo-desktop">
          Betsabé <br />
          Meneses
        </span>
      </router-link>
      <div class="right-buttons">
        <LocaleSwitcher />
        <router-link 
          to="/about" 
          class="btn-secondary" 
        >
          <span class="underlined-02">{{ $t("buttonProfile") }}</span>
        </router-link>
        <router-link 
          to="/contact"
          class="btn-secondary"  
        >
          <span class="underlined-02">{{ $t("buttonContact") }}</span>
        </router-link>
      </div>
    </nav>

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

    <nav class="nav-mobile">
      <router-link to="/" @click="toggleMenu()" class="btn-nav-mobile">
        Home
      </router-link>
      <router-link to="/about" @click="toggleMenu()" class="btn-nav-mobile">
       {{ $t("buttonProfile") }} 
      </router-link>
      <router-link 
          to="/contact"
          class="btn-nav-mobile"
          @click="toggleMenu()"  
        >
          CONTACT
      </router-link>
      <LocaleSwitcher class="languages-mobile" 
      />
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
      let navbar = document.querySelector(".nav-desktop")

      window.addEventListener("scroll", function () {
        if (window.scrollY > 0) {
          navbar.classList.add("scrolled");
        } else {
          navbar.classList.remove("scrolled");
        }
      });
    },
      // showingNavbar() {
      //   const navbar = document.querySelector(".nav-desktop");
      //   if (window.scrollY > 0 && !this.isOpen) {
      //     navbar.classList.add("scrolled");
      //   } else {
      //     navbar.classList.remove("scrolled");
      //   }
      // },

    toggleMenu() {
      this.isOpen = !this.isOpen;
      this.openMenu();
    },
    openMenu() {
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
  z-index: 20;
  height: 85px;
  border-bottom: 0.5px solid transparent;
}
nav.scrolled {
  background: var(--white-bg);
  border-bottom: var(--linesStyle);
}
.btn-name {
  width: 15%;
}
.btn-name span {
  line-height: 17px;
  font-size: 18px;
  padding: 2px;
  font-weight: 600;
}
.right-buttons {
  display: flex;
  width: 35%;
}
.btn-secondary,
.btn-name {
  display: flex;
  justify-content: center;
  align-items: center;
  transition: all 0.5s ease;
}
.btn-secondary {
  width: 33%;
}
.btn-secondary span {
  text-transform: uppercase;
  font-size: 15px;
  padding: 5px 8px;
  font-weight: 600;
}
.btn-secondary:hover {
  background-size: 100% 2px;
}
.nav-desktop {
  opacity: 0;
}
.logo-mobile {
  display: none;
}

/* burguer menu */
.btn-burguer-ctn{
  position: fixed;
  top: 35px;
  right:40px;  
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
  height: 2px;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  background-color: var(--grey1);
  transition: all 0.3s ease-in-out;  
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
  z-index: 35;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  border: var(--linesStyle);
}
.nav-mobile.active {
  opacity: 1;
}
.btn-nav-mobile{
  font-size: 25px;
  font-family: "Inter", sans-serif;
  text-transform: uppercase;
  margin-bottom: 10px;
}

.languages-mobile {
  margin-top: 15px;
}

@media only screen and (max-width: 768px) {
  .right-buttons {
    display: none;
  }
  .btn-burguer-ctn {
    display: block;
  }
  .btn-burguer{
    z-index: 50;
  }
  .btn-name,
  .btn-secondary {
    width: 25%;
    border: none;
  }
}
@media only screen and (max-width: 480px) { 
  .btn-name{
    width: 50px;
    margin-left: 20px;
  } 
  .btn-name p {
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
  .btn-burguer-ctn {
    right: 30px;
  }
  .btn-nav-mobile {
    font-size: 18px;
  }
}
</style>
