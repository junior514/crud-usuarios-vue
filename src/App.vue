<template>
    <div id="app">
        <!-- Header -->
        <div class="header-section">
            <div class="container">
                <h1 class="text-center mb-0">Gestión de Usuarios</h1>
                <p class="text-center mb-0 opacity-75">Sistema CRUD con Vue.js</p>
            </div>
        </div>

        <div class="container">
            <!-- Loading Spinner -->
            <LoadingSpinner v-if="loading" />

            <!-- Main Content -->
            <div v-else>
                <!-- Add User Button -->
                <div class="d-flex justify-content-between align-items-center mb-4">
                    <h3>Lista de Usuarios ({{ users.length }})</h3>
                    <button class="btn btn-primary btn-lg" @click="openAddModal">
                        <i class="bi bi-plus-circle"></i> Agregar Usuario
                    </button>
                </div>

                <!-- Users Table -->
                <UserTable :users="users" @edit-user="openEditModal" @confirm-delete="confirmDelete" />
            </div>
        </div>

        <!-- Add/Edit User Modal -->
        <UserModal ref="userModal" :is-editing="isEditing" :current-user="currentUser" @save-user="saveUser"
            @modal-hidden="resetForm" />

        <!-- Delete Confirmation Modal -->
        <DeleteModal ref="deleteModal" :user-to-delete="userToDelete" @confirm-delete="deleteUser" />
    </div>
</template>

<script>
import UserTable from './components/UserTable.vue'
import UserModal from './components/UserModal.vue'
import DeleteModal from './components/DeleteModal.vue'
import LoadingSpinner from './components/LoadingSpinner.vue'

export default {
    name: 'App',
    components: {
        UserTable,
        UserModal,
        DeleteModal,
        LoadingSpinner
    },
    data() {
        return {
            users: [],
            loading: true,
            isEditing: false,
            currentUser: {
                id: null,
                name: '',
                username: '',
                email: '',
                phone: ''
            },
            userToDelete: null
        }
    },
    async mounted() {
        await this.fetchUsers()
    },
    methods: {
        async fetchUsers() {
            try {
                this.loading = true
                const response = await fetch('https://jsonplaceholder.typicode.com/users')
                if (!response.ok) {
                    throw new Error('Error al cargar los usuarios')
                }
                this.users = await response.json()
            } catch (error) {
                console.error('Error fetching users:', error)
                alert('Error al cargar los usuarios. Por favor, intenta de nuevo.')
            } finally {
                this.loading = false
            }
        },

        openAddModal() {
            this.isEditing = false
            this.currentUser = {
                id: null,
                name: '',
                username: '',
                email: '',
                phone: ''
            }
            this.$refs.userModal.show()
        },

        openEditModal(user) {
            this.isEditing = true
            this.currentUser = { ...user }
            this.$refs.userModal.show()
        },

        saveUser(userData) {
            if (this.isEditing) {
                // Actualizar usuario existente
                const index = this.users.findIndex(u => u.id === userData.id)
                if (index !== -1) {
                    this.users[index] = { ...userData }
                }
            } else {
                // Agregar nuevo usuario
                const newId = Math.max(...this.users.map(u => u.id)) + 1
                const newUser = {
                    ...userData,
                    id: newId
                }
                this.users.push(newUser)
            }

            this.$refs.userModal.hide()
        },

        confirmDelete(user) {
            this.userToDelete = user
            this.$refs.deleteModal.show()
        },

        deleteUser() {
            if (this.userToDelete) {
                const index = this.users.findIndex(u => u.id === this.userToDelete.id)
                if (index !== -1) {
                    this.users.splice(index, 1)
                }
                this.userToDelete = null
                this.$refs.deleteModal.hide()
            }
        },

        resetForm() {
            this.currentUser = {
                id: null,
                name: '',
                username: '',
                email: '',
                phone: ''
            }
            this.isEditing = false
        }
    }
}
</script>

<style>
.header-section {
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    color: white;
    padding: 2rem 0;
    margin-bottom: 2rem;
}

.card {
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
    border: none;
}

.btn-primary {
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    border: none;
}

.btn-primary:hover {
    background: linear-gradient(135deg, #5a6fd8 0%, #6a4190 100%);
}

.btn-action {
    margin: 0 2px;
}
</style>
