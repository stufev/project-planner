<template>
  <div class="project__container" :class="{'project__container-complete': project.complete}">
    <div class="project__top">
      <div class="project__title" @click="showDescription = !showDescription">{{ project.title }}</div>
      <div class="project__icons">
        <div class="project__icon-edit">
          <router-link :to="{name: 'edit', params: {id: project.id}}">
            <img src="src/assets/icons/edit.svg" alt="">
          </router-link>
        </div>
        <div class="project__icon-remove" @click="deleteProject">
          <img src="src/assets/icons/delete.svg" alt="">
        </div>
        <div class="project__icon-complete" :class="{'project__icon-complete-done': project.complete}"
             @click="completeProject">
          <img src="src/assets/icons/complete.svg" alt="">
        </div>
      </div>
    </div>
    <div class="project__description" v-if="showDescription">
      {{ project.details }}
    </div>
  </div>
</template>

<script>
export default {
  props: ['project'],
  data() {
    return {
      showDescription: false,
      uri: 'http://localhost:3000/projects/' + this.project.id
    }
  },
  methods: {
    completeProject() {
      fetch(this.uri, {
        method: 'PATCH',
        headers: {'Content-Type': 'application/json'},
        body: JSON.stringify({'complete': !this.project.complete})
      }).then(() => {
        this.$emit('toggleComplete', this.project.id)
      }).catch((err) => {
        console.log(err.message)
      })
    },
    deleteProject() {
      fetch(this.uri, {method: 'DELETE'})
          .then(() => this.$emit('handleDelete', this.project.id))
          .catch((err => {
            console.log(err.message)
          }))
    }
  }
}
</script>

<style scoped>
.project__container {
  width: 600px;
  margin: 20px auto;
  background: white;
  padding: 10px 20px;
  border-radius: 4px;
  box-shadow: 1px 2px 3px rgb(0 0 0 / 5%);
  border-left: 4px solid #e90074;
}

.project__container-complete {
  border-color: #00ce89;
}

.project__top {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding-top: 20px;
  padding-bottom: 20px;
}

.project__title {
  max-width: 450px;
  font-weight: 700;
  cursor: pointer;
  user-select: none;
}

.project__icons {
  display: flex;
}

.project__icons img {
  width: 30px;
  height: 20px;
  cursor: pointer;
  opacity: 0.5;
  transition: .2s all linear;
}

.project__icons img:hover {
  opacity: 1;
}

.project__description {
  padding-top: 10px;
  padding-bottom: 20px;
}

.project__icon-complete-done img {
  opacity: 1;
  filter: invert(44%) sepia(88%) saturate(1478%) hue-rotate(92deg) brightness(107%) contrast(106%);
}
</style>