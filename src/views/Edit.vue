<template>
  <form @submit.prevent="submitForm">
    <label>Title</label>
    <input v-model="title" required>
    <label>Details</label>
    <textarea v-model="details" placeholder="details..." required></textarea>
    <button>Edit Project</button>
  </form>
</template>

<script>
export default {
  name: 'edit',
  props: ['id'],
  data() {
    return {
      title: '',
      details: '',
      uri: 'http://localhost:3000/projects/' + this.id
    }
  },
  methods: {
    submitForm() {
      fetch(this.uri, {
        method: 'PATCH',
        headers: {'Content-Type': 'application/json'},
        body: JSON.stringify({title: this.title, details: this.details})
      }).then(() => {
        this.$router.push('/');
      }).catch((err) => {
        console.log(err.message);
      })
    }
  },
  mounted() {
    fetch(this.uri).then((res) => {
      return res.json();
    }).then((data) => {
      this.title = data.title;
      this.details = data.details;
    }).catch((err) => {
      console.log(err.message);
    })
  }
}
</script>

<style>

</style>