<template>
  <div class="home">
    <div v-if="projects.length">
      <div v-for="project in projects" :key="project.id">
        <SingleProject :project="project" @delete="filterProjects" @complete="completeProjects"/>
      </div>
    </div>
    
  </div>
</template>

<script>

import SingleProject from "../components/SingleProject.vue"
export default {

  name: 'Home',
  components: {
    SingleProject
  },

  data() {
    return {
      projects: [],
    }
  },

  methods: {
    filterProjects(id) {
      this.projects = this.projects.filter(project => project.id != id);
    },

    completeProjects(id) {
      let project = this.projects.find(project => {return project.id == id});
      project.complete = !project.complete;
    }
  },

  mounted() {
    fetch('http://localhost:3000/projects')
    .then(response => response.json())
    .then(response => this.projects = response)
    .catch(error => console.log(error))
  }
}
</script>
