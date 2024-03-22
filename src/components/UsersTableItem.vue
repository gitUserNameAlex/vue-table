<template>
    <tr>
        <td>
            <v-text-field v-model="editedItem.firstName" :readonly="!editing" variant="plain" />
        </td>
        <td>
            <v-text-field v-model.number="editedItem.age" :readonly="!editing" variant="plain"/>
        </td>
        <td class="text-center">
            <v-btn v-if="!editing" @click="editMode(true)" variant="outlined" color="primary" class="ma-2">
                Редактировать
            </v-btn>
            <v-btn v-else @click="saveChanges" variant="outlined" color="success" class="ma-2">
                Сохранить
            </v-btn>
            <v-btn @click="$emit('delete', item)" variant="outlined" color="error" class="ma-2">
                Удалить
            </v-btn>
        </td>
    </tr>
</template>
<script>

export default {
    props: {
        item: {
            type: Object,
            required: true
        }
    },

    data() {
        return {
            editing: false,
            editedItem: { ...this.item }
        };
    },

    methods: {
        editMode(status) {
            this.editing = status;
        },

        saveChanges() {
            this.$emit("update", this.editedItem);
            this.editMode(false);
        },
    },
}
</script>

<style scoped>

</style>