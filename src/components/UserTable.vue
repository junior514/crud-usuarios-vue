<template>
    <div class="card table-container">
        <div class="card-body p-0">
            <div class="table-responsive">
                <table class="table table-hover mb-0">
                    <thead class="table-dark">
                        <tr>
                            <th>ID</th>
                            <th>Nombre</th>
                            <th>Usuario</th>
                            <th>Email</th>
                            <th>Teléfono</th>
                            <th class="text-center">Acciones</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr v-for="user in users" :key="user.id">
                            <td>{{ user.id }}</td>
                            <td>{{ user.name }}</td>
                            <td>{{ user.username }}</td>
                            <td>{{ user.email }}</td>
                            <td>{{ user.phone }}</td>
                            <td class="text-center">
                                <button class="btn btn-warning btn-sm btn-action" @click="$emit('edit-user', user)">
                                    Editar
                                </button>
                                <button class="btn btn-danger btn-sm btn-action" @click="$emit('confirm-delete', user)">
                                    Eliminar
                                </button>
                            </td>
                        </tr>
                    </tbody>
                </table>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'UserTable',
    props: {
        users: {
            type: Array,
            required: true
        }
    },
    emits: ['edit-user', 'confirm-delete']
}
</script>

<style scoped>
.table-container {
    margin-top: 20px;
}

.btn-action {
    margin: 0 2px;
}
</style>
