<template>
  <HeaderNav/>
  <router-view/>
</template>

<script>
import HeaderNav from "@/components/HeaderNav.vue"
export default {
  components: {
    HeaderNav
  }
}
</script>

<style>
*,
*::before,
*::after {
  box-sizing: border-box;
}

html {
  line-height: 1.15; /* 1 */
  -webkit-text-size-adjust: 100%; /* 2 */
}

body {
  font-family: 'Roboto', sans-serif;
  margin: 0;
  background: #f2f2f2;
  font-size: 18px;
}

a {
  background-color: transparent;
}

button,
input,
optgroup,
select,
textarea {
  font-family: inherit; /* 1 */
  font-size: 100%; /* 1 */
  line-height: 1.15; /* 1 */
  margin: 0; /* 2 */
}

#app {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>
