<template>
  <div class="project">
    <div class="actions">
      <h3 @click="detailsVisible = !detailsVisible">{{ project.title }}</h3>
      <div class="icons">
        <span class="material-icons"> edit </span>
        <span class="material-icons"> delete </span>
         <span class="material-icons"> done </span>
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
    };
  },
  props: ["project"],
  methods: {
    // toggleDetails() {
    //   this.detailsVisible = !this.detailsVisible;
    // }
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

h3 {
  cursor: pointer;
}

.icons {
  float: right;
  display: inline;
}
</style>