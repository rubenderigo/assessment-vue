<template>
  <div class="container">
    <ActorTable :actors="actors"/>
  </div>
</template>

<script>
import ActorTable from "@/components/ActorTable";

export default {
  name: 'App',
  components: {
    ActorTable,
  },
  data() {
    return {
      actors: [],
      isEditing: false,
    }
  },
  methods: {
    async fetchActors() {
      const res = await fetch('https://data.cinetica-tech.com/test/api/actors')
      const data = await res.json()
      return data
    }
  },
  async created() {
    this.actors = await this.fetchActors()
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
