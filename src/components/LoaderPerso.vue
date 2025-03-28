<template>
    <div  class="loader-bg">
        <div class="progress-container">
          <div class="progress">
            <div ref="progressBar" class="progress-bar"></div>
          </div>
        </div>
    </div>
</template>

<script>
import { ref, onMounted} from "vue";
import gsap from "gsap";

export default {
  name: "LoaderPerso",
  setup(_, { emit }) { // Recibir `emit` correctamente en Vue 3
    const progressBar = ref(null);

    onMounted(() => {
      gsap
        .timeline()
        .to(progressBar.value, { duration: 1.2, width: "100%", ease: "power1.out" })
        .to(".loader-bg", { duration: 0.4, opacity: 0, ease: "power1.out", onComplete: () => {
          emit("loaded"); // 🔥 Emitimos el evento "loaded" cuando termine la animación
        }});
    });

    return { progressBar };
  },
  emits: ["loaded"], // ✅ Definir el evento para evitar advertencias en Vue 3
};
</script>

<style>
.loader-bg {
  position: fixed;
  width: 100%;
  height: 100%;
  background-color: var(--black);
  z-index: 999;
  opacity: 1;
}
.progress-container {
	left: 50%;
  top:50%;
	position: absolute;
	transform: translate(-50%, -50%);    
}
.progress {
	background-color: #000;
	height: 0.25em;
	position: relative;
	width: 190px;
}
.progress-bar {
	background-size: 23em 0.25em;
	height: 100%;
	position: relative;
  background-color: var(--pink);
  width: 0;
}

</style>
