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
        </div>
      </div>
    </div>

    <div class="content">
      <div
        v-for="single in singleProject.infoByProject"
        :key="single.id"
        class="bloc-project"
      >
        <div class="text-bloc">
          <h4>{{ single.title }}</h4>
          <p v-if="single.paragraph">{{ single.paragraph }}</p>
        </div>
        <img
          :src="single.img"
          :alt="singleProject.alt"
          class="bloc-project-images"
        />
      </div>

      <div class="btn-info-ctn">
        <a
          class="btn-info underlined-02"
          :href="singleProject.link"
          target="_blank"
          >🔎En savoir plus
        </a>
      </div>
    </div>
    <div class="change-project">
      <div>
        <p class="underlined-02" @click="goBack">Previous project</p>
      </div>
      <div>
        <p class="underlined-02" @click="goFoward">Next project</p>
      </div>
    </div>
  </div>
</template>

<script>
import data from "../data";
export default {
  name: "SingleProject",
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
        this.$router.replace({ path: "/" + nextId });
      }
    },
    goBack() {
      let prevId = parseInt(this.currentId) - 1;

      if (prevId < 1) {
        return;
      } else {
        this.$router.replace({ path: "/" + prevId });
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
.text-bloc {
  padding: 10px 40px;
}
.introduction-bloc {
  display: flex;
}
.left-bloc,
.right-bloc {
  width: 50%;
  padding: 60px 40px;
}
.left-bloc p,
.left-bloc ul {
  margin: 0;
}
.left-bloc h5,
.right-bloc h5 {
  margin: 22px 0 7px;
}
.right-bloc p,
.text-bloc p {
  line-height: 23px;
}
.left-bloc ul {
  display: flex;
  padding: 0;
  flex-wrap: wrap;
}
.left-bloc li {
  list-style: none;
  margin-right: 5px;
}
.bloc-project {
  margin: 60px 0;
}
.bloc-project-images {
  width: 100%;
  object-fit: contain;
  position: relative;
  padding: 0 1px;
}
.btn-info-ctn {
  padding: 10px 40px;
  display: flex;
  justify-content: flex-end;
  margin-bottom: 30px;
}
.btn-info {
  display: inline-block;
  font-size: 15px;
  font-family: "Montserrat", sans-serif;
  font-weight: 600;
  color: var(--grey1);
  text-transform: uppercase;
  cursor: pointer;
  margin: 10px;
  padding: 5px 0;
}
.head-image-mobile {
  display: none;
}
.change-project {
  display: flex;
  justify-content: center;
  align-items: center;
  color: var(--grey1);
  font-weight: 600;
  text-transform: uppercase;
  position: relative;
  width: 35%;
  margin: 0 auto;
}
.change-project div:first-child,
.change-project div:last-child {
  width: 50%;
  cursor: pointer;
  padding: 0 20px;
}
.change-project p {
  padding: 5px;
  text-align: center;
  width: fit-content;
  margin: 0 auto;
}

@media only screen and (max-width: 768px) {
  .introduction-bloc,
  .content {
    width: 80%;
    margin: auto 10%;
  }
  .introduction-bloc {
    flex-direction: column;
  }
  .left-bloc,
  .right-bloc,
  .text-bloc {
    width: 100%;
    padding: 0 20px;
  }
  .head-image-container {
    margin-top: 65px;
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
  .text-bloc h4,
  .introduction-bloc h5 {
    margin: 12px 0;
  }
  .head-image-container {
    height: 300px;
    margin-top: 55px;
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
}
</style>
