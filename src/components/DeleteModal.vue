<template>
    <div class="modal fade" id="deleteModal" tabindex="-1" ref="deleteModal">
        <div class="modal-dialog">
            <div class="modal-content">
                <div class="modal-header">
                    <h5 class="modal-title">Confirmar Eliminación</h5>
                    <button type="button" class="btn-close" data-bs-dismiss="modal"></button>
                </div>
                <div class="modal-body">
                    <p>¿Estás seguro de que deseas eliminar al usuario <strong>{{ userToDelete?.name }}</strong>?</p>
                    <p class="text-muted">Esta acción no se puede deshacer.</p>
                </div>
                <div class="modal-footer">
                    <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Cancelar</button>
                    <button type="button" class="btn btn-danger" @click="confirmDelete">Eliminar</button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import { Modal } from 'bootstrap'

export default {
    name: 'DeleteModal',
    props: {
        userToDelete: {
            type: Object,
            default: null
        }
    },
    emits: ['confirm-delete'],
    data() {
        return {
            modal: null
        }
    },
    mounted() {
        this.modal = new Modal(this.$refs.deleteModal)
    },
    methods: {
        show() {
            this.modal.show()
        },

        hide() {
            this.modal.hide()
        },

        confirmDelete() {
            this.$emit('confirm-delete')
        }
    }
}
</script>
