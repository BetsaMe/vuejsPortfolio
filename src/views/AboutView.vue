<template>
    <section class="about">
        <div class="circle-container">
            <div class="circle3"></div>
        </div>        
        <div class="center-bloc-about anim-2">
            <div class="about-text">
              <h4>{{ $t("about") }}</h4>
              <p class="anim-2">{{ $t("aboutP1") }}</p>
              <p class="anim-2">{{ $t("aboutP2") }}</p>
              <p class="anim-2">{{ $t("aboutP3") }}</p>
              <p class="anim-2">{{ $t("aboutP4") }}</p>
              <div class="ctn-btn-download anim-2">
                  <DownloadBtn 
                    href="images/CV-Betsa-2022.pdf"
                    download="CV-Betsa-2022"
                    title="Download cv"
                  />  
              </div>
            </div>
            <div class="profile-photo-ctn">
              <img src="images/profile2.webp" alt="profilepicture" class="anim-2 profile-photo" />
            </div>
        </div>   
    </section>
</template>

<script>
import gsap from "gsap";
import DownloadBtn from "@/components/DownloadBtn.vue"
export default {
    name: "AboutView",
    components:{
        DownloadBtn
    },
    mounted() {
        this.aboutAnimation();
        
    },
    methods: {
        aboutAnimation() {
          let tl = gsap.timeline();
          tl.to(".anim-2", { stagger: 0.1, opacity: 1, duration: 1, y: 0,ease: "power2.inOut" })
            .to(".circle3", {opacity: 0.6, duration: 0.7 ,ease: "power2.inOut" });
        }
    },
};
</script>

<style>
.anim-2 {
  opacity: 0;
  transform: translateY(40px);
}
.about{
  position: relative;
  z-index: 14;
  min-height: 100vh;
}

/* About section */
.center-bloc-about {
  width: 70%;
  margin: 0 15% 40px;
  padding: 125px 0 50px;
  display: flex;
  justify-content: space-between;
}
.about-text{
  padding: 0 40px;
  width: 50%;
}
.about-text p{
  font-size: 17px;
  line-height: 24px;
}
.about-text > h4{
  font-family: 'Inter', sans-serif;
  font-weight: 200;
  font-size: 5vw;
  line-height: 100%;
  margin:20px 0 30px;
}
.profile-photo-ctn{
  width: 50%;
  display: flex;
  justify-content: center;
  align-items: center;
}
.profile-photo {
  object-fit: cover;
  width: 350px;  
  height: 400px;
  border: solid 1px var(--grey3);
}
.circle3 {
  width: 550px;
  height: 550px;
  position: absolute;
  opacity: 0;
  top:50px;
  right: 80px;
  background: radial-gradient(190px, #96f5e8, transparent);
}
.ctn-btn-download{
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  margin-top:60px;
}

@media only screen and (max-width: 1024px) {
  .center-bloc-about {
    flex-direction: column;
  }
  .profile-photo-ctn{
    width: 100%;
  }
  .about-text {
    width: 100%;
  }
  .about-text > h4{
    font-size: 8vw;
}
  .profile-photo {
    margin: auto;
    padding: 0;
  }
  .ctn-btn-download{
    margin-bottom:70px;
  }
}
@media screen and (max-width: 768px) {
  .center-bloc-about {
    width: 80%;
    margin: 0 10% 40px;
    padding: 105px 0 0;
  }
}
@media screen and (max-width: 480px) {
  .center-bloc-about {
    width: 100%;
    margin: 0;
    padding: 75px 0;
  }
  .about-text {
    padding: 20px;
  }
  .ctn-btn-download{
    margin: 0px;
  }
  .profile-photo {
    width: 100%;
    height: 350px;
  }
  .about-text > h4{
    font-size: 12vw;
  }
}
</style>
