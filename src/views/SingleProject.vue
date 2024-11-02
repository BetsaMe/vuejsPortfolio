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
          <h5>Catégorie</h5>
          <p>{{ singleProject.subtitle }}</p>
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
          <a class="partner-style" v-if="singleProject.partner" :href="singleProject.partner" target="_blank">Andrea Galindo</a>
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
          <h4>{{ single.title }}</h4>
          <p v-if="single.paragraph">{{ single.paragraph }}</p>
        </div>
        <img
          :src="single.img"
          :alt="singleProject.alt"
          class="project-paragraph-images"
        />
      </div>

      <div class="btn-info-ctn">
        <DownloadBtn 
          :title="singleProject.lastButton"
          :href="singleProject.link"
          target="_blank"
        />
      </div>
    </div>
    <ul class="change-project">
        
        <li  @click="goBack"> 
            <ArrowBtn title="Previous" arrowPosition="before">
            </ArrowBtn>
        </li>   
     
        <li  @click="goFoward">
          <ArrowBtn title="Next" arrowPosition="after">
          </ArrowBtn>
        </li>      
    </ul>
  </div>
</template>

<script>
import data from "../data.js"
import DownloadBtn from "@/components/DownloadBtn.vue";
import ArrowBtn from "@/components/ArrowBtn.vue";
export default {
  name: "SingleProject",
  components:{
        DownloadBtn,
        ArrowBtn
  },
  data() {
    return {
      projets: data,
      singleProject: null,
      currentId: this.$route.params.projetId,
    };
  },
  created() {
    this.getSingleProjet();
  },
  computed: {
    paramsId() {
      return this.$route.params.projetId;
    },
  },
  methods: {
    getSingleProjet() {
      this.singleProject = this.projets.filter(
        (projet) => projet.id === parseInt(this.paramsId)
      )[0];
    },
    goFoward() {
      let nextId = parseInt(this.currentId) + 1;

      if (nextId > this.projets.length) {
        return;
      } else {
        this.$router.replace({ path: "/work/" + nextId });
      }
    },
    goBack() {
      let prevId = parseInt(this.currentId) - 1;

      if (prevId < 1) {
        return;
      } else {
        this.$router.replace({ path: "/work/" + prevId });
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
.left-bloc p{
  margin: 0 0 35px;
}
.left-bloc ul {
  margin: 0;
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
  padding: 40px ;
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
  justify-content:flex-end; 
  margin: 10px;
}

.head-image-mobile {
  display: none;
}
.change-project {
  display: flex;
  justify-content: center;
  width: 33%;
  font-weight: 600;
  text-transform: uppercase;
  position: relative;
  margin: 80px auto ;
  padding: 0;
}
.change-project li:first-child,
.change-project li:last-child {
  width: 50%;
  cursor: pointer;
  display: flex;
  justify-content: space-around;
}
.change-project span {
  padding: 5px;
  text-align: center;
  width: fit-content;
}
.partner-style{
  font-weight: 500;
  text-decoration: underline;

}

@media only screen and (max-width: 768px) {
  .introduction-bloc,
  .content {
    width: 80%;
    margin: auto 10%;
  }
  .introduction-bloc{
    margin-bottom: 40px;
    flex-direction: column;
  }
  .left-bloc,
  .right-bloc
  {
    width: 100%;
    padding: 20px;
  }
  .project-paragraph {
    margin: 0 0 70px;  
  }
  .text-bloc{
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
  .project-paragraph{
    margin-bottom: 60px;
  }
  .introduction-bloc{
    margin-bottom: 40px;
  }
  .text-bloc{
    padding: 20px;
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
    justify-content:center; 
  }
}
</style>
