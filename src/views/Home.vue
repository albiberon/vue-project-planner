<template>
  <div class="home">
    <h1>Project Planner</h1>
    <div v-if="projects.length">
      <div v-for="project in projects" :key="project.id">
        <SingleProject :project="project"/>
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
};
</script>
