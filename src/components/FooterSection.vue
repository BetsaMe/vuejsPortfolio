<template>
    <section id="contact">
        <div class="circle-container-footer">
            <div class="circle4"></div>
        </div>
        <div class="contact">
            <div class="bloc-contact">        
                <p>Contact</p>
                <ul>
                  <li v-for="link in links" :key="link" class="underlined-02">
                      <a :href="link.link" target="_blank">{{ link.name }}</a>
                  </li>
                </ul>
            </div>
        </div>
        <div class="creator">
            <span class="">© {{ new Date().getFullYear() }} Betsabé M</span>
        </div>
    </section>
</template>

<script>
import gsap from "gsap";
import ScrollTrigger from "gsap/ScrollTrigger";

export default {
  name: "FooterSection",
  data() {
    return {
      links: [
        { name: "Github", link: "https://github.com/BetsaMe" },
        {
          name: "Linkedin",
          link: "https://www.linkedin.com/in/betsab%C3%A9-m-4972178b/",
        },
        { name: "Behance", link: "https://www.behance.net/betsameneses" },
        { name: "Email me", link: "mailto: betsamene@gmail.com" },
      ],
    };
  },
  mounted() {
    ScrollTrigger.refresh();
    gsap.registerPlugin(ScrollTrigger);
    this.parallaxContact();
  },
  methods: {
    parallaxContact() {
      let mm = gsap.matchMedia();
      mm.add("(min-width: 800px)", () =>{
        gsap.to(".bloc-contact p", {
            x: 120,
            scrollTrigger: {
              trigger: ".contact",
              start: "top center+=200",
              scrub: 1
            },
          });
      })
    },
  },
};
</script>

<style>
/* Contact section */
#contact .circle-container-footer{
  position: absolute;
  width: 100%;
  height: 40vh;
  overflow: hidden; 
  bottom: 0;
}
.contact {
  display: flex;
  width: 100%;
  height: 40vh;
  position: relative;
  justify-content: center;
  align-content: center;
}
.bloc-contact {
  width: 70%;
  display: flex;
  overflow: hidden;
  z-index: 30;
}
.bloc-contact p,
.bloc-contact ul {  
  padding: 0;
  margin: 0;  
}
.bloc-contact p {
  font-family: 'Inter', sans-serif;
  font-weight: 200;
  font-size: 120px;
  line-height: 90%;  
  align-self: flex-end;
  position: relative;
  bottom: -33px;
  width: 75%;
}
.bloc-contact ul {
  height: 100%;
  z-index: 1;
  list-style: none;
  display: flex;
  flex-direction: column;
  align-items:flex-start;
  justify-content: center;
  width: 25%;
  padding-left: 10px;
}
.bloc-contact li {
  font-size: 17px;
  font-weight: 500;
  padding: 3px;
  margin:5px 0;
}
.creator {
  font-size: 13px;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 30px;
  width: 100%;
  border-bottom: var(--linesStyle);
  border-top: var(--linesStyle);
}

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
.circle4 {
  width: 400px;
  height: 400px;
  position: absolute;
  bottom: -150px;
  left: 0;
  opacity: 0.5;
  background: radial-gradient(200px, #c5c6ff, transparent);
}
@media only screen and (max-width: 768px) {
  .contact {
    margin-top: 50px;
  }
  .bloc-contact {
    width: 80%;
  }
  .bloc-contact p {
    font-size: 100px;
    bottom: -30px;
  }
}
@media only screen and (max-width: 480px) {
  .contact {
    height: 30vh;
  }
  .bloc-contact {
    width: 100%;
    padding: 0 20px;
    flex-direction: column;
  }
  .bloc-contact :nth-child(1) {
    order: 2;
  }
  .bloc-contact p {
    font-size: 65px;
    bottom: -16px;
    text-align: center;
    width: 100%;
  }
  .bloc-contact ul {
    width: 100%;
    align-items:center;
    padding: 8px 0 0;
  }
  .bloc-contact li {
    margin: 5px;
    font-size: 15px;
  }
}
</style>
