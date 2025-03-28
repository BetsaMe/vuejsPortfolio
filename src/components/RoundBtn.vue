<template>
  <div>
    <a
      href="images/CV-Betsa-Meneses.pdf"
      download="CV-Betsa"
      class="ctn-round-btn"
    >
      <div class="center-dot"><span>cv</span></div>
      <img
        class="txt-animated fade-in-left"
        src="/images/textocircularv2.png"
        alt="circular text"
      />
    </a>
  </div>
</template>

<script>
import gsap from "gsap";

export default {
  name: "RoundBtn",
  mounted() {
    this.displayDot();
    console.log("this is mounted");
    
  },
  methods: {
    displayDot() {
      gsap.set(".center-dot", { opacity: 1 }); // Asegura el estado inicial

      gsap.from(
        ".center-dot",
        {
          opacity: 0,
          duration: 0.2,
          ease: "Power1.easeOut",
          delay: 3, // 🔥 Retraso de 3 segundos antes de iniciar la animación

        },
      );
    },
  },
};
</script>

<style>
.ctn-round-btn {
  width: 200px;
  height: 200px;
  position: absolute;
  bottom: 0px;
  right: calc(15% - 100px);
  display: flex;
  justify-content: center;
  align-items: center;
}

.txt-animated {
  width: 200px;
  height: 200px;
  position: relative;
}

.center-dot {
  position: absolute;
  width: 55px;
  height: 55px;
  background-color: var(--grey2);
  z-index: 40;
  border-radius: 50%;
  transform-origin: center; /* Asegura que el origen esté en el centro */
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%) scale(0.05); /* Incluye scale(1) para el estado inicial */
  transition: transform 0.3s ease-in-out;
  display: flex;
  justify-content: center;
  align-items: center;
}
.center-dot span {
  color: white;
}
.ctn-round-btn:hover .center-dot {
  transform: translate(-50%, -50%) scale(2); /* Expande desde el centro */
}

@media screen and (max-width: 1024px) {
  .ctn-round-btn {
    bottom: -50px;
  }
}

@media only screen and (max-width: 768px) {
  .ctn-round-btn {
    width: 160px;
    height: 160px;
    bottom: -40px;
  }
  .ctn-round-btn:hover .center-dot {
  transform: translate(-50%, -50%) scale(1.6); /* Expande desde el centro */
}
  .txt-animated {
    width: 160px;
    height: 160px;
  }
}

@media screen and (max-width: 480px) {
  .ctn-round-btn {
    height: 140px;
    bottom: -20px;

  }
  .ctn-round-btn:hover .center-dot {
  transform: translate(-50%, -50%) scale(1.4); /* Expande desde el centro */
}
  .txt-animated {
    width: 140px;
    height: 140px;

  }
}
</style>
