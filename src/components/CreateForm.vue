<template>
  <v-form @submit.prevent>
    <v-responsive class="text-center mx-auto" width="100%" max-width="350">

        <v-text-field v-model="user.firstName" label="Имя" class="ma-1" color="success" variant="solo"/>
        <v-text-field v-model="user.age" label="Возраст" class="ma-1" color="success" variant="solo"/>

        <v-btn @click="createUser" type="submit" color="green">
          Добавить пользователя
        </v-btn>

    </v-responsive>
  </v-form>
</template>

<script>
export default {
  props: {
    tableData: {
      type: Array,
      required: true,
    }
  },

  data() {
    return {
      user: {
        firstName: '',
        age: null,
      }
    }
  },

  methods: {
    createUser() {
      this.user.id = this.tableData.length+1
      this.user.age = parseInt(this.user.age)
      this.$emit('create',this.user)
      this.user = {
        firstName: '',
        age: null,
      }
    }
  }
  
}
</script>

<style scoped>
  
</style>