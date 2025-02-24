<template>
    <div class="r-modal" v-if="show" id="client-modal">
        <div class="r-modal-content">
            <div class="r-modal-header">
                <h5>{{ this.client !== null ? "Editar" : "Criar" }} Cliente<span class="close" @click="closeModal()">&times;</span></h5>
            </div>
            <form>
                <div class="mb-3">
                    <label for="inFirstName" class="form-label">Primeiro Nome</label>
                    <input type="text" class="form-control" id="inFirstName" :value="client?.firstName"/>
                </div>
                <div class="mb-3">
                    <label for="inLastName" class="form-label">Último Nome</label>
                    <input type="text" class="form-control" id="inLastName" :value="client?.lastName"/>
                </div>
                <div class="mb-3">
                    <label for="inEmail" class="form-label">E-Mail</label>
                    <input type="email" class="form-control" id="inEmail" :value="client?.email" required/>
                </div>
                <button class="btn btn-secondary" @click="closeModal()">Fechar</button>
                <button class="btn btn-primary" type="submit">Gravar</button>
            </form>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            client: null,
            show: false
        }
    },
    methods: {
        showModal(client) {
            this.client = client;
            this.show = true;
        },
        closeModal() {
            this.client = null;
            this.show = false;
        }
    }
}
</script>