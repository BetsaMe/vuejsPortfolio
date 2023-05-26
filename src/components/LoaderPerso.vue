<template>
    <div class="loader-bg">
        <div class="progress-container">
          <div class="progress">
              <div class="progress-bar">                
              </div>
          </div>
        </div>
    </div>
</template>

<script>
import gsap from "gsap";
export default {
  name: 'LoaderPerso',
    mounted() {
      this.loaderAnim();
  },
  methods: {
    loaderAnim(){
      let tl = gsap.timeline();
      tl.to(".progress-bar", { duration:1.2, width: "100%", ease: "power1.out"})
        .to(".loader-bg", { duration:0.4, opacity: 0, display:"none", ease: "power1.out"})
    }    
	} 
}
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
