<template>
  <div class="home">
    <h1>Project Planner</h1>
    <div v-if="projects.length">
      <div v-for="project in projects" :key="project.id">
        <SingleProject :project="project" @delete="handleDelete" @complete="handleComplete"/>
      </div>
    </div>
    <div v-else>
      <p>Projects loading</p>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import SingleProject from "../components/SingleProject.vue"

export default {
  name: "Home",
  data() {
    return {
      projects: [],
    };
  },
  components: { SingleProject },
  mounted() {
    fetch("http://localhost:3000/projects")
      .then((res) => res.json())
      .then((data) => (this.projects = data))
      .catch((err) => console.log(err.message));
  },
  methods: {
    handleDelete(id) {
      this.projects = this.projects.filter((project)=>{
        return project.id !== id
      })
    },
    handleComplete(id) {
      let p = this.projects.find(project => {
        return project.id === id
      })
      p.complete = !p.complete
    }
  }
};
</script>
