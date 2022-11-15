<template>
  <div class="navigation__title">
    <router-link to="/">
      <h1>VUE PROJECT PLANNER</h1>
    </router-link>
  </div>
  <nav class="navigation__menu">
    <router-link to="/">Projects</router-link>
    <router-link to="/add">Add a New Project</router-link>
  </nav>
</template>

<script>
</script>

<style scoped>
.navigation__title {
  text-align: center;
}

.navigation__title a {
  color: #222;
  text-decoration: none;
}

.navigation__menu {
  margin-bottom: 20px;
}

.navigation__menu {
  text-align: center;
  margin: 40px auto;
}

.navigation__menu a {
  display: inline-block;
  text-decoration: none;
  margin: 0 10px;
  color: #999;
  font-size: 18px;
}

a.router-link-active {
  border-bottom: 2px solid #00ce89;
  padding-bottom: 4px;
}

</style>
