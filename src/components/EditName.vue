<template>
  <div>
    <form @submit="onSubmit" class="d-flex w-90 justify-content-center">
      <div>
        <input type="text" class="form-control" :value="nameActor" @change="onChange">
      </div>
      <button type="submit" class="btn btn-primary">Submit</button>
    </form>
    {{status}}
  </div>
</template>

<script>
export default {
  name: "EditName",
  props: {
    actor: Object,
    nameActor: String,
  },
  data() {
    return {
      newName: '',
      status: '',
      valueInput: ''
    }
  },
  methods: {
    onChange(event) {
      this.newName = event.target.value
    },
    async onSubmit(event) {
      event.preventDefault()
      const res = await fetch('https://data.cinetica-tech.com/test/api/actors', {
        method: 'POST',
        headers: {
          Accept: 'application/json',
          'Content-Type': 'application/json',
        },
        body: JSON.stringify({ id: this.actor.id, name: this.newName }),
      });
      res.status === 200 ? (this.$emit('name-changed', this.newName)) : this.status = "error to change name"
    }
  }
}
</script>

<style scoped>
input {
  width: 150px;
  min-width: 100px;
}
</style>