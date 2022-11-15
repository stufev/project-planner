<template>
  <nav class="filter-nav">
    <button @click="setFilter('all')" :class="{active: currentCond === 'all'}">All Projects</button>
    <button @click="setFilter('complete')" :class="{active: currentCond === 'complete'}">Complete</button>
    <button @click="setFilter('ongoing')" :class="{active: currentCond === 'ongoing'}">Ongoing</button>
  </nav>
</template>

<script>
export default {
  props: ['currentCond'],
  methods: {
    setFilter(cond) {
      this.$emit('getFilter', cond)
    }
  }
}
</script>

<style>
.filter-nav button {
  background: none;
  border: none;
  color: #bbb;
  outline: none;
  font-size: 12px;
  text-transform: uppercase;
  letter-spacing: 1px;
  font-weight: bold;
  cursor: pointer;
}

.filter-nav button.active {
  color: #555;
}

</style>