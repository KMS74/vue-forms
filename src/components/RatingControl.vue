<template>
  <ul>
    <li :class="{ active: rate === 'poor' }">
      <button type="button" v-on:click="activate('poor')">Poor</button>
    </li>
    <li :class="{ active: rate === 'ave' }">
      <button type="button" v-on:click="activate('ave')">Average</button>
    </li>
    <li :class="{ active: rate === 'good' }">
      <button type="button" v-on:click="activate('good')">Good</button>
    </li>
  </ul>
</template>

<script>
export default {
  props: ['rate'],
  emits: ['update:rate'],
  methods: {
    activate(option) {
      this.$emit('update:rate', option);
    },
  },
};
</script>
option

<style scoped>
.active {
  border-color: #0076bb;
}
.active button {
  color: #0076bb;
}
ul {
  list-style-type: none;
  margin: 0.5rem auto;
  padding: 0;
  display: flex;
}
li {
  margin: 0 1rem;
  border: 1px solid #ccc;
  padding: 0.5rem;
  display: flex;
  justify-content: center;
  align-items: center;
}

button {
  font: inherit;
  border: none;
  background-color: transparent;
  cursor: pointer;
}
</style>
