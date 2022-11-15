<template>
  <Filter @getFilter="filterProjects" :current-cond="currentCond"/>
  <div class="home__projects" v-if="projects.length">
    <SingleProject v-for="project in filteredProjects" :project="project" @toggleComplete="toggleComplete"
                   @handleDelete="handleDelete"/>
  </div>
</template>

<script>
import SingleProject from "@/components/SingleProject.vue";
import Filter from "@/components/Filter.vue";

export default {
  components: {SingleProject, Filter},
  data() {
    return {
      projects: [],
      currentCond: 'all'
    }
  },
  computed: {
    filteredProjects() {
      if (this.currentCond === 'complete') {
        return this.projects.filter(project => project.complete === true);
      }
      if (this.currentCond === 'ongoing') {
        return this.projects.filter(project => project.complete === false);
      }
      return this.projects;
    }
  },
  methods: {
    toggleComplete(id) {
      let findProj = this.projects.find(project => project.id === id);
      findProj.complete = !findProj.complete;
    },
    handleDelete(id) {
      this.projects = this.projects.filter(project => project.id !== id);
    },
    filterProjects(cond) {
      this.currentCond = cond;
    }
  },
  mounted() {
    fetch("http://localhost:3000/projects/")
        .then(res => res.json())
        .then(data => this.projects = data)
        .catch((err) => {
          console.log(err.message)
        })
  }
}
</script>

<style>
</style>
