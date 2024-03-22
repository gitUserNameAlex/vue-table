<template>
    <v-table>

        <thead>
          <tr>
            <th class="text-left" style="font-weight: 600;">
                Имя
            </th>
            <th class="text-left" style="font-weight: 600;">
              Возраст
            </th>
            <th class="text-center" style="font-weight: 600;">
              Действия
            </th>
          </tr>
        </thead>

        <tbody>
            <users-table-item v-for="item in tableData" :item="item" :key="item.id" @delete="$emit('delete', item)"/>
        </tbody>

    </v-table>
</template>

<script>
import UsersTableItem from './UsersTableItem.vue'

export default {
    components: {
        UsersTableItem
    },

    props: {
        tableData: {
            type: Array,
            required: true
        }
    }
}
</script>

<style scoped>
    
</style>