<template>
  <form @submit.prevent="submitForm">
    <label>Title</label>
    <input v-model="title" required>
    <label>Details</label>
    <textarea v-model="details" placeholder="details..." required></textarea>
    <button>Add Project</button>
  </form>
</template>

<script>
export default {
  name: 'add',
  data() {
    return {
      title: '',
      details: ''
    }
  },
  methods: {
    submitForm() {
      const obj = {
        // id: Math.floor(Math.random() * 10000),
        title: this.title,
        details: this.details,
        complete: false
      }

      fetch('http://localhost:3000/projects', {
        method: 'POST',
        headers: {'Content-Type': 'application/json'},
        body: JSON.stringify(obj)
      }).then(() => {
        this.$router.push('/');
      }).catch((err) => {
        console.log(err.message);
      })

    }
  }
}
</script>

<style>
form {
  background: white;
  padding: 20px;
  border-radius: 10px;
  max-width: 650px;
  width: 100%;
}

label {
  display: block;
  color: #bbb;
  text-transform: uppercase;
  font-size: 14px;
  font-weight: bold;
  letter-spacing: 1px;
  margin: 20px 0 10px 0
}

input {
  padding: 10px;
  border: 0;
  border-bottom: 1px solid #ddd;
  width: 100%;
  box-sizing: border-box;
}

textarea {
  border: 1px solid #ddd;
  padding: 10px;
  width: 100%;
  box-sizing: border-box;
  height: 100px;
  resize: none;
}

form button {
  display: block;
  margin: 20px auto 0;
  background: #00ce89;
  color: white;
  padding: 10px;
  border: 0;
  border-radius: 6px;
  font-size: 16px;
}
</style>