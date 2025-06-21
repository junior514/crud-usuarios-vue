<template>
    <div class="modal fade" id="userModal" tabindex="-1" ref="userModal">
        <div class="modal-dialog modal-lg">
            <div class="modal-content">
                <div class="modal-header">
                    <h5 class="modal-title">{{ isEditing ? 'Editar Usuario' : 'Agregar Usuario' }}</h5>
                    <button type="button" class="btn-close" data-bs-dismiss="modal"></button>
                </div>
                <div class="modal-body">
                    <form @submit.prevent="saveUser">
                        <div class="row">
                            <div class="col-md-6">
                                <div class="form-floating">
                                    <input type="text" class="form-control" :class="{ 'is-invalid': errors.name }"
                                        id="name" v-model="formData.name" placeholder="Nombre completo" required>
                                    <label for="name">Nombre completo</label>
                                    <div v-if="errors.name" class="invalid-feedback">
                                        {{ errors.name }}
                                    </div>
                                </div>
                            </div>
                            <div class="col-md-6">
                                <div class="form-floating">
                                    <input type="text" class="form-control" :class="{ 'is-invalid': errors.username }"
                                        id="username" v-model="formData.username" placeholder="Nombre de usuario"
                                        required>
                                    <label for="username">Nombre de usuario</label>
                                    <div v-if="errors.username" class="invalid-feedback">
                                        {{ errors.username }}
                                    </div>
                                </div>
                            </div>
                        </div>
                        <div class="row">
                            <div class="col-md-6">
                                <div class="form-floating">
                                    <input type="email" class="form-control" :class="{ 'is-invalid': errors.email }"
                                        id="email" v-model="formData.email" placeholder="Email" required>
                                    <label for="email">Email</label>
                                    <div v-if="errors.email" class="invalid-feedback">
                                        {{ errors.email }}
                                    </div>
                                </div>
                            </div>
                            <div class="col-md-6">
                                <div class="form-floating">
                                    <input type="tel" class="form-control" :class="{ 'is-invalid': errors.phone }"
                                        id="phone" v-model="formData.phone" placeholder="Teléfono" required>
                                    <label for="phone">Teléfono</label>
                                    <div v-if="errors.phone" class="invalid-feedback">
                                        {{ errors.phone }}
                                    </div>
                                </div>
                            </div>
                        </div>
                    </form>
                </div>
                <div class="modal-footer">
                    <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Cancelar</button>
                    <button type="button" class="btn btn-primary" @click="saveUser" :disabled="!isFormValid">
                        {{ isEditing ? 'Actualizar' : 'Guardar' }} Usuario
                    </button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import { Modal } from 'bootstrap'

export default {
    name: 'UserModal',
    props: {
        isEditing: {
            type: Boolean,
            default: false
        },
        currentUser: {
            type: Object,
            required: true
        }
    },
    emits: ['save-user', 'modal-hidden'],
    data() {
        return {
            formData: {
                id: null,
                name: '',
                username: '',
                email: '',
                phone: ''
            },
            errors: {},
            modal: null
        }
    },
    computed: {
        isFormValid() {
            return this.formData.name &&
                this.formData.username &&
                this.formData.email &&
                this.formData.phone &&
                this.isValidEmail(this.formData.email) &&
                Object.keys(this.errors).length === 0
        }
    },
    watch: {
        currentUser: {
            handler(newUser) {
                this.formData = { ...newUser }
                this.errors = {}
            },
            deep: true,
            immediate: true
        }
    },
    mounted() {
        this.modal = new Modal(this.$refs.userModal)
        this.$refs.userModal.addEventListener('hidden.bs.modal', () => {
            this.$emit('modal-hidden')
        })
    },
    methods: {
        show() {
            this.modal.show()
        },

        hide() {
            this.modal.hide()
        },

        validateForm() {
            this.errors = {}

            if (!this.formData.name.trim()) {
                this.errors.name = 'El nombre es requerido'
            }

            if (!this.formData.username.trim()) {
                this.errors.username = 'El nombre de usuario es requerido'
            }

            if (!this.formData.email.trim()) {
                this.errors.email = 'El email es requerido'
            } else if (!this.isValidEmail(this.formData.email)) {
                this.errors.email = 'El email no tiene un formato válido'
            }

            if (!this.formData.phone.trim()) {
                this.errors.phone = 'El teléfono es requerido'
            }

            return Object.keys(this.errors).length === 0
        },

        isValidEmail(email) {
            const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/
            return emailRegex.test(email)
        },

        saveUser() {
            if (!this.validateForm()) {
                return
            }

            this.$emit('save-user', { ...this.formData })
        }
    }
}
</script>

<style scoped>
.modal-content {
    border-radius: 10px;
}

.form-floating {
    margin-bottom: 15px;
}

.invalid-feedback {
    display: block;
}
</style>
