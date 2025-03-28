<template>
  <section id="hero">
    <div class="center-bloc">
      <span class="box-star4">
        <img class="star4" src="/images/star4.svg" alt="star" />
        <span>{{ $t("grettings") }}</span>
        <img class="star4" src="/images/star4.svg" alt="star" />
      </span>
      <h1>
        <span class="par-1">{{ $t("firstLineH1") }}</span>
        <span class="par-2">& {{ $t("secondLineH1") }}</span>
      </h1>
      <p class="fade-in description">
        {{ $t("description") }}
        <span class="highlightText">{{ $t("txtcolor") }}</span>
      </p>

      <div class="box-animated-text">
        <RoundBtn />
      </div>
    </div>
  </section>
</template>

<script>
import gsap from "gsap";
import RoundBtn from "./RoundBtn.vue";
export default {
  name: "HelloWorld",
  components: { RoundBtn },
  mounted() {
    this.heroAnimation();
  },
  methods: {
    heroAnimation() {
      let tl = gsap.timeline();
      // Animación de las dos líneas del h1 con un pequeño delay entre ellas
      tl.from(".box-star4", {
        opacity: 0,
        duration: 0.7,
        y: 20,
        ease: "power1.out",
      })

        .from(".par-1", {
          opacity: 0,
          y: 40,
          duration: 0.8,
          ease: "power1.out",
        })
        .from(
          ".par-2",
          {
            opacity: 0,
            y: 40,
            duration: 0.8,
            ease: "power1.out",
          },
          "-=0.5"
        ) // Empieza antes de que termine la anterior para un efecto más fluido

        .to(
          ".fade-in",
          {
            opacity: 1,
            duration: 0.7,
            y: 0,
            ease: "power1.out",
          },
          "-=0.5"
        )
        .to(
          ".highlightText",
          {
            backgroundSize: "100% 100%", // Expande el subrayado
            duration: 0.7,
            ease: "power1.out",
          },
          "-=0.3"
        ) // Empieza un poco antes del final de la animación anterior
        .to(
          ".fade-in-left",
          {
            opacity: 1,
            rotation: 45, // Rotación en grados
            duration: 0.7,
            x: 0,
            ease: "Power1.easeOut",
          },
          
        )
        .to(".fade-in-left", {
          opacity: 1,
          rotation: "+=360", // Rotación en grados
          duration: 16, // Duración en segundos
          repeat: -1, // Repetición infinita
          ease: "linear",
        });
    },
  },
};
</script>

<style>
/* Hero section */

h1,
h2,
h3 {
  font-family: "pp_eikothin", sans-serif;
  font-weight: normal;
}
h1 {
  font-size: 9vw;
  letter-spacing: -0.02em;
  text-align: center;
  margin: 0;
}
#hero {
  /* display: flex; */
  width: 100%;
  min-height: 100vh;
  margin: auto;
  position: relative;
}
.center-bloc {
  margin: 0 auto;
  width: 100%;
  padding: 135px 0;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  overflow: hidden;
}

/* lineas del h1 */
.par-1,
.par-2 {
  display: block;
}
.description {
  font-size: 1.15em;
  line-height: 1.5em;
  width: 30%;
  margin-top: 60px;
  text-align: center;
  color: #868585;
}

.box-animated-text {
  /*caja externa*/
  position: relative;
  width: 100%;
  height: 100px;
  top: 0;
  right: 0;
}

.box-star4 {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-bottom: 20px;
}
.star4 {
  height: 14px;
  margin: 0 5px;
}
.highlightText {
  background-image: linear-gradient(180deg, #adbaff, #adbaff);
  background-repeat: no-repeat;
  background-size: 0.2em 100%; /* Estado inicial pequeño */
  background-position: 0 88%;
  color: var(--grey2);
}
.fade-in {
  opacity: 0;
  transform: translateY(65px);
}
.fade-in-left {
  opacity: 0;
  transform: translateX(50px);
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
  .center-bloc {
    background-color: transparent;
    width: 80%;
    padding-bottom: 80px;
  }

  h1 {
    font-size: 10vw;
  }
}

@media screen and (max-width: 480px) {
  .center-bloc {
    width: 100%;
    margin: 0;
    padding: 100px 20px 0px;
    height: 100vh;
  }
  .description {
    width: 100%;
    margin-top: 30px;
  }
  h1 {
    font-size: 48px;
  }

  .box-star4 span {
    font-size: 15px;
  }
}
</style>
