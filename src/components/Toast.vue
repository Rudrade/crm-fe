<template>
    <div class="toast-container position-fixed bottom-0 end-0 p-3">
        <div id="toast" class="toast" role="alert" aria-live="assertive" aria-atomic="true">
            <div class="toast-header">
                <i class="bi bi-dash-circle" style="margin-right: 5%; color: red" v-if="isError"></i>
                <strong class="me-auto" style="color: red" v-if="isError">Erro</strong>
                
                <i class="bi bi-check-circle" style="margin-right: 5%; color: green" v-if="!isError"></i>
                <strong class="me-auto" style="color: green" v-if="!isError">Sucesso</strong>
                
                <button type="button" class="btn-close" data-bs-dismiss="toast" aria-label="Close" @click="$emit('closeToast')"></button>
            </div>
            <div class="toast-body" :style="style">
                {{ message }}
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        isError: {
            type: Boolean,
            required: true
        },
        message: String
    },
    computed: {
        style() {
            return {
                color: this.isError ? "red" : "green"
            }
        }
    }
}
</script>