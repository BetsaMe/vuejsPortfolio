<template>
  <div id="single-project">
    <div class="head-image-container">
      <img
        :src="singleProject.coverImage"
        :alt="singleProject.alt"
        class="head-image head-image-mobile"
      />
      <img
        :src="singleProject.headImage"
        :alt="singleProject.alt"
        class="head-image head-image-desktop"
      />
    </div>

    <div class="single-project-bloc">
      <div class="introduction-bloc">
        <div class="left-bloc">
          <h5>Category</h5>
          <ul class="tech-label-container scroll-content">
            <li
              class="tech-label"
              v-for="element in singleProject.tags"
              :key="element"
            >
              {{ element }}
            </li>
          </ul>
          <!-- <p>{{ singleProject.subtitle }}</p> -->
          <h5>Rol</h5>
          <p>{{ singleProject.rol }}</p>
          <h5>Year</h5>
          <p>{{ singleProject.year }}</p>
          <h5>Outils</h5>
          <ul>
            <li
              v-for="single in singleProject.techno"
              :key="single.id"
              class=""
            >
              {{ single }}
            </li>
          </ul>
        </div>
        <div class="right-bloc">
          <h5>Brief</h5>
          <p>{{ $t(singleProject.resume) }}</p>
          <a
            class="partner-style"
            v-if="singleProject.partner"
            :href="singleProject.partner"
            target="_blank"
            >Andrea Galindo</a
          >
        </div>
      </div>
    </div>

    <div class="content">
      <div
        v-for="single in singleProject.infoByProject"
        :key="single.id"
        class="project-paragraph"
      >
        <div class="text-bloc">
          <h4>{{ $t(single.title) }}</h4>
          <p v-if="single.paragraph">{{ $t(single.paragraph) }}</p>
        </div>
        <img
          :src="single.img"
          :alt="singleProject.alt"
          class="project-paragraph-images"
        />
      </div>
      <a
        :href="singleProject.link"
        target="_blank"
        class="btn-info-ctn"
        v-if="singleProject.link"
      >
        <DownloadBtn
          title="saber más"
          :bgColor="'#fff'"
          :textColor="'#616fe4'"
          :borderColor="'#616fe4'"
          :hoverBgColor="'#616fe4'"
          :hoverTextColor="'#fff'"
          :hoverBorderColor="'#616fe4'"
        />
      </a>
    </div>
    <ul class="change-project">
      <div class="go-back" @click="goBack">
        <img src="/images/arrow-left.svg" alt="arrow" />
        <li>previous</li>
      </div>
      <div class="move-foward" @click="goForward">
        <img src="/images/arrow-right.svg" alt="arrow" />
        <li>next</li>
      </div>
    </ul>
  </div>
</template>

<script>
import data from "../data.js";
import DownloadBtn from "@/components/DownloadBtn.vue";
export default {
  name: "SingleProject",
  components: {
    DownloadBtn,
  },
  data() {
    return {
      projets: data,
      singleProject: null,
    };
  },
  created() {
    this.getSingleProjet();
  },
  computed: {
    paramsSlug() {
      return this.$route.params.slug;
    },
  },
  methods: {
    getSingleProjet() {
      this.singleProject = this.projets.find(
        (projet) => projet.slug === this.paramsSlug // Comparamos con slug
      );

      if (!this.singleProject) {
        console.error("Proyecto no encontrado:", this.paramsSlug);
        this.$router.push("/404"); // Redirige a una página de error si no se encuentra
      }
    },
    goForward() {
      // Encuentra el índice del proyecto actual en el array
      const currentIndex = this.projets.findIndex(
        (projet) => projet.slug === this.paramsSlug
      );
 
      if (currentIndex !== -1 && currentIndex < this.projets.length - 1) {
        const nextProject = this.projets[currentIndex + 1];
        this.$router.push({
          name: "single",
          params: { slug: nextProject.slug },
        });
      }
    },
    goBack() {
      const currentIndex = this.projets.findIndex(
        (projet) => projet.slug === this.paramsSlug
      );
      console.log(currentIndex);

      if (currentIndex > 0) {
        const prevProject = this.projets[currentIndex - 1];
        this.$router.push({
          name: "single",
          params: { slug: prevProject.slug },
        });
      }
    },
  },
};
</script>

<style>
.head-image-container {
  margin: 86px 0 0;
  height: 60vh;
  width: 100%;
  position: relative;
  z-index: 6;
}
.head-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
}
.single-project-bloc {
  width: 100%;
  border-top: var(--linesStyle);
}
.introduction-bloc,
.content {
  width: 70%;
  margin: auto 15%;
  position: relative;
}
.introduction-bloc {
  display: flex;
}
.left-bloc,
.right-bloc {
  width: 50%;
  padding: 60px 40px;
}
.left-bloc p {
  margin: 0 0 35px;
}
.left-bloc ul {
  margin: 0 0 35px;
  display: flex;
  padding: 0;
  flex-wrap: wrap;
}
.left-bloc li {
  margin-right: 6px;
}
.left-bloc h5,
.right-bloc h5 {
  margin: 4px 0;
}
.right-bloc p {
  line-height: 23px;
  margin: 0;
}
/* Project content */
.project-paragraph {
  margin: 0 0 100px;
}
.text-bloc {
  padding: 40px;
  width: 50%;
}
.text-bloc h4 {
  margin: 4px 0;
}
.text-bloc p {
  margin: 0;
  line-height: 23px;
}
.project-paragraph-images {
  width: 100%;
  object-fit: contain;
  position: relative;
  padding: 0 1px;
}
.btn-info-ctn {
  display: flex;
  justify-content: flex-end;
  margin: 10px;
}

.head-image-mobile {
  display: none;
}

/* Ir al siguiente proyecto */
.change-project {
  display: flex;
  justify-content: space-evenly;
  width: 33%;
  font-weight: 600;
  text-transform: uppercase;
  position: relative;
  margin: 80px auto;
  padding: 0;
}
.change-project img {
  height: 35px;
}
.change-project li {
  text-decoration: underline;
}
.go-back,
.move-foward {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  width: 80px;
  cursor: pointer;
}
.go-back:hover,
.move-foward:hover {
  color: #616fe4;
}
.partner-style {
  color: #616fe4;
  text-decoration: underline;
}
@media only screen and (max-width: 768px) {
  .introduction-bloc,
  .content {
    width: 80%;
    margin: auto 10%;
  }
  .introduction-bloc {
    margin-bottom: 40px;
    flex-direction: column;
  }
  .left-bloc,
  .right-bloc {
    width: 100%;
    padding: 20px;
  }
  .project-paragraph {
    margin: 0 0 70px;
  }
  .text-bloc {
    padding: 30px 20px;
  }
  .head-image-mobile {
    display: block;
  }
  .head-image-desktop {
    display: none;
  }
  .change-project {
    width: 80%;
  }
}
@media only screen and (max-width: 480px) {
  .introduction-bloc,
  .content {
    margin: 0;
    width: 100%;
  }
  .project-paragraph {
    margin-bottom: 60px;
  }
  .introduction-bloc {
    margin-bottom: 40px;
  }
  .text-bloc {
    padding: 20px;
    width: 100%;
  }
  .head-image-container {
    height: 300px;
  }
  .head-image {
    height: 300px;
  }
  .change-project {
    width: 100%;
    margin-bottom: 30px;
    padding: 0 20px;
  }
  .change-project p {
    font-size: 13px;
  }
  .btn-info-ctn {
    justify-content: center;
  }
}
</style>
