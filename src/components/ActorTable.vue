<template>
  <div class="table-responsive text-center">
    <table class="table table-bordered table-striped">
      <thead>
      <tr>
        <th scope="col">#</th>
        <th scope="col">ID</th>
        <th scope="col">Picture</th>
        <th scope="col">Name</th>
        <th scope="col">Gender</th>
        <th scope="col">Age</th>
        <th scope="col"></th>
      </tr>
      </thead>
      <tbody>
      <tr v-for="(actor, index ) in actors" :key="actor.id">
        <ActorItem :actor="actor" :index="index"/>
      </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import ActorItem from "@/components/ActorItem";

export default {
  name: 'ActorTable',
  props: {
    actors: Array,
    isEditing: Boolean,
  },
  components: {
    ActorItem
  }
}
</script>