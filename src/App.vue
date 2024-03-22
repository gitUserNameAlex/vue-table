<template>
  <v-app>
    <v-container>

      <users-table :tableData="tableData" @update="updateUser" @delete="deleteUser" />

      <create-form @create="createUser" :tableData="tableData"/>

    </v-container>
  </v-app>
</template>

<script>
  import axios from 'axios'
  import UsersTable from './components/UsersTable.vue'
  import CreateForm from './components/CreateForm.vue'

  export default {
    name: 'App',

    components: {
      UsersTable, CreateForm
    },
    
    data() {
      return {
        tableData: [],
      }
    },
    
    methods: {
      async fetchUsers() {
        try {
          const response = await axios.get('https://dummyjson.com/users?limit=8')
          this.tableData = response.data.users
        }
        catch(err) {
          console.log('Error while fetching users:', err)
        }
      },

      createUser(user) {
        this.tableData.push(user)
      },

      updateUser(updatedUser) {
        const index = this.tableData.findIndex(user => user.id === updatedUser.id);
        this.tableData[index] = { ...updatedUser };
      },

      deleteUser(userToDelete) {
        this.tableData = this.tableData.filter((user) => user.id !== userToDelete.id)
      },
    },

    mounted() {
      this.fetchUsers()
    }
  }
</script>

<style>
*{
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
</style>