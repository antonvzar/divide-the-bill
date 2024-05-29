<template>
  <form @submit.prevent>
    <h4>Add the guest</h4>
    <my-input
      v-focus
      v-model="guest.name"
      type="text"
      placeholder="Имя"
    />
    <my-input
      v-model="guest.surname"
      type="text"
      placeholder="Фамилия"
    />
    <my-button
      style="align-self: flex-end; margin-top: 15px"
      @click="createGuest"
    >
      Создать
    </my-button>
  </form>
</template>

<script>
export default {
  data() {
    return {
      guest: {
        name: '',
        surname: ''
      }
    }
  },
  methods: {
    createGuest() {
      this.guest.id = Date.now();
      this.$emit('create', this.guest)
      this.guest = {
        name: '',
        surname: ''
      }
    }
  },
}
</script>

<style scoped>
form {
  display: flex;
  flex-direction: column;
}

</style>
