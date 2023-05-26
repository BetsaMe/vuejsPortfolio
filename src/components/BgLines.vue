<template>
  <div class="bg-lines">
    <div class="line line-1"></div>
    <div class="line line-2"></div>
    <div class="line line-3"></div>
    <div class="line line-4"></div>
    <div class="line line-5"></div>
    <div class="line line-6"></div>
  </div>
</template>

<script>
import gsap from "gsap";
export default {
  name: "BgLines",
  mounted(){
    gsap.to(".bg-lines", { duration:1.2, opacity: 1, ease: "power2.out"});
  }
};
</script>

<style>
.bg-lines {
  width: 100%;
  height: 100%;
  position: absolute;
  top: 0;
  display: flex;
  opacity: 0;
}
.line {
  position: relative;  
  background-color: transparent;
  border-right: 0.5px solid var(--grey4);
}
.line-1, .line-6{
  width: 15%;
}
.line-2, .line-3, .line-4, .line-5{
  width: 17.5%;
}

@media only screen and (max-width: 768px) {
  .line-1, .line-6{
    display: none;  
  }
  .line-2, .line-5{
    width: 10%;
  }
  .line-4, .line-3{
    width: 40%;
  }
}
@media screen and (max-width: 480px) {
  .bg-lines {
    display: none;
  }
}
</style>
