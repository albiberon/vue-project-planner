<template>
  <div class="project" :class="{ complete : project.complete }">
    <div class="actions">
      <h3 @click="detailsVisible = !detailsVisible">{{ project.title }}</h3>
      <div class="icons">
        <router-link :to="{ name: 'EditProject', params: { id: project.id }}">
          <span class="material-icons" @click="editProject"> edit </span>
        </router-link>
        <span class="material-icons" @click="deleteProject"> delete </span>
        <span class="material-icons tick" @click="toggleComplete"> done </span>
      </div>
    </div>
    <div v-if="detailsVisible" class="details">
      <p>{{ project.details }}</p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      detailsVisible: false,
      uri: "http://localhost:3000/projects/" + this.project.id,
    };
  },
  props: ["project"],
  methods: {
    deleteProject() {
      fetch(this.uri, { method: "DELETE" })
        .then(() => this.$emit("delete", this.project.id))
        .catch((err) => console.log(err))
    },
    toggleComplete() {
      fetch(this.uri, {
        method: "PATCH",
        headers: { 'Content-Type' : 'application/json' },
        body: JSON.stringify({ complete: !this.project.complete })
        })
          .then( () => this.$emit("complete" , this.project.id) )
          .catch( (err) => console.log(err) )
    }
  },
};
</script>

<style>
.project {
  margin: 20px auto;
  background: white;
  padding: 10px 20px;
  border-radius: 4px;
  box-shadow: 1px 2px 3px rgba (0, 0, 0, 0.05);
  border-left: 4px solid #e90074;
  text-align: left;
}

.project.complete {
  border-left: 4px solid #00ce89;
}

h3 {
  cursor: pointer;
  display: inline-block;
}

.material-icons {
  font-size: 24px;
  margin-left: 10px;
  color: #bbb;
  cursor: pointer;
}

.material-icons:hover {
  color: #777;
}

.icons {
    display: inline-block;
    float: right;
    padding-top: 20px;
}

.project.complete .tick {
  color: #00ce89;
}
</style>