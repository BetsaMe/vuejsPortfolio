<template>
    <div>
        <LoaderPerso v-if="loading"/>
        <div v-else>       
          <BgLines />
          <div class="cursor cursor--small"></div>
          <MenuBar />
          <router-view :key="$route.path"/>
          <FooterSection />      
        </div>
    </div>  
</template>

<script>
import LoaderPerso from "@/components/LoaderPerso.vue";
import MenuBar from "@/components/MenuBar.vue";
import FooterSection from "@/components/FooterSection.vue";
import BgLines from "@/components/BgLines.vue";

export default {
  name: "App",
  components: {
    MenuBar,
    FooterSection,
    BgLines,
    LoaderPerso
  },
  data() {
    return {
      loading: true,
      offset:0
    };
  },
  created() {
    document.title = "Betsabé Meneses";
  },
  mounted(){
      setTimeout(() => (this.loading = false), 1650);
  }
};
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@400;500;600;700&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@100;200;300;400&family=Overpass:wght@100;200;300;400&display=swap');
@import url('https://fonts.googleapis.com/css2?family=DM+Sans:ital,opsz,wght@0,9..40,100..1000;1,9..40,100..1000&display=swap');

@font-face {
    font-family: 'pp_eiko_italiclight';
    src: url('./fonts/eiko-font/ppeiko-lightitalic-webfont.woff2') format('woff2'),
         url('./fonts/eiko-font/ppeiko-lightitalic-webfont.woff') format('woff');
    font-weight: normal;
    font-style: normal;
    font-display: swap; /* Añadido para evitar problemas */
}

@font-face {
    font-family: 'pp_eikomedium';
    src: url('./fonts/eiko-font/ppeiko-medium-webfont.woff2') format('woff2'),
         url('./fonts/eiko-font/ppeiko-medium-webfont.woff') format('woff');
    font-weight: normal;
    font-style: normal;

} 

@font-face {
    font-family: 'pp_eikothin';
    src: url('./fonts/eiko-font/ppeiko-thin-webfont.woff2') format('woff2'),
         url('./fonts/eiko-font/ppeiko-thin-webfont.woff') format('woff');
    font-weight: normal;
    font-style: normal;

}

:root {
  --black: #212121;
  --grey1: #696969;
  --grey2: #444444;
  --grey3: #cbcccf;
  --grey4: #e0e0e0;
  --white-bg: #fbfaf9;
  --pink: #f1a1e3;
  --linesStyle: solid 0.5px var(--grey4);
}

* {
  box-sizing: border-box;
}
html {
  scroll-behavior: smooth;
  cursor: none;
  font-size: 100%;
}

body {
  height: 100%;
  font-family: "Montserrat", sans-serif;
  font-weight: 400;
  background-color: var(--white-bg);
  margin: 0;
  padding: 0;
  position: relative;
  color: var(--grey2);
  cursor:url("/public/images/cursor.svg"), auto;
}
a {
  text-decoration: none;
  color: var(--black);
}
ul{
  list-style: none;
}
@media screen and (max-width: 480px) {
  .cursor {
    display: none;
  }
  html {
    cursor: default;
  }

}
</style>
