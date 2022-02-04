<template>
  <th scope="col">{{ index + 1 }}</th>
  <th scope="col">{{ actor.id }}</th>
  <th scope="col">
    <img :src="actor.picture" width="90"/>
  </th>
  <th v-if="isEditing">
    <EditName :actor="actor" @name-changed="refresh" :nameActor="nameActor"/>
  </th>
  <th v-else> {{ nameActor }}</th>
  <th scope="col">{{ getGender(actor.gender) }}</th>
  <th scope="col">{{ getAge(actor.bornDate) }}</th>
  <th scope="col">
    <button @click="onClick" type="button" class="btn btn-primary">Edit</button>
  </th>
</template>

<script>
import EditName from "@/components/EditName";

export default {
  name: "ActorItem",
  props: {
    actor: Object,
    index: Number,
  },
  components: {
    EditName,
  },
  data() {
    return {
      isEditing: false,
      nameActor: ''
    }
  },
  methods: {
    getAge(dateBorn) {
      const today = new Date();
      const actorDate = new Date(dateBorn);
      const age = today.getFullYear() - actorDate.getFullYear();
      const diferenceBetweenMonths = today.getMonth() - actorDate.getMonth();
      const isMonthDiference = diferenceBetweenMonths < 0;
      const idDayDiference = diferenceBetweenMonths === 0 && today.getDate() < actorDate.getDate();

      return isMonthDiference || idDayDiference ? age - 1 : age;
    },
    getGender(gender) {
      return gender === "M" ? 'Actor' : "Actress"
    },
    onClick(event) {
      event.preventDefault()
      this.isEditing = !this.isEditing
    },
    refresh(newName) {
      this.isEditing = !this.isEditing
      this.nameActor = newName
    }
  },
  created() {
    this.nameActor = this.actor.name
  }
}
</script>