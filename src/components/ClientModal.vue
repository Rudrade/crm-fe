<template>
    <div class="r-modal" v-if="show" id="client-modal">
        <div class="r-modal-content">
            <div class="r-modal-header">
                <h5>{{ this.client !== null ? "Editar" : "Criar" }} Cliente<span class="close" @click="closeModal()">&times;</span></h5>
            </div>
            <div class="mb-3">
                <label for="inFirstName" class="form-label">Primeiro Nome</label>
                <input type="text" class="form-control" id="inFirstName" v-model="client.firstName"/>
            </div>
            <div class="mb-3">
                <label for="inLastName" class="form-label">Último Nome</label>
                <input type="text" class="form-control" id="inLastName" v-model="client.lastName"/>
            </div>
            <div class="mb-3">
                <label for="inEmail" class="form-label">E-Mail</label>
                <input type="email" class="form-control" id="inEmail" v-model="client.email"/>
            </div>
            <button class="btn btn-secondary" @click="closeModal()">Fechar</button>
            <button class="btn btn-primary" @click="postClient()">Gravar</button>
        </div>
    </div>
</template>

<script>
import axios from 'axios';

export default {
    data() {
        return {
            client: {
                id: 0,
                firstName: "",
                lastName: "",
                email: ""
            },
            show: false
        }
    },
    props: {
        showToast: Function
    },
    methods: {
        showModal(client) {
            if (client !== undefined) {
                this.client = { ...client };
            }
            this.show = true;
        },
        closeModal() {
            this.client = null;
            this.show = false;
        },
        postClient() {
            console.log("creating cliente");

            const client = this.client;
            console.log(client)
            if (client === null) {
                return;
            }

            axios.post("http://localhost:8080/crm/api/client", 
                client
            )
            .then(() => {
                this.showToast("Cliente "+(this.client.id===0?"criado":"atualizado")+" com sucesso.", false);
                this.closeModal();
            });
        }
    }
}
</script>