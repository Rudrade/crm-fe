<template>
    <table class="table table-hover table-bordered border-dark-subtle">
        <thead>
            <tr>
                <th>ID</th>
                <th>Primeiro Nome</th>
                <th>Último Nome</th>
                <th>E-mail</th>
                <th>Ações</th>
            </tr>
        </thead>
        <tbody class="table-group-divider">
            <tr v-for="client in clients" :key="client.id">
                <td>{{ client.id }}</td>
                <td>{{ client.firstName }}</td>
                <td>{{ client.lastName }}</td>
                <td>{{ client.email }}</td>
                <td><button class="btn btn-secondary" @click="openModalClient(client)"><i class="bi bi-pencil-square"></i></button></td>
            </tr>
        </tbody>
        <div v-if="clients.length === 0" style="color: red; font-weight: bold;" class="">
            Sem dados
        </div>
    </table>

    <button class="btn btn-secondary" @click="openModalClient(null)">Criar Cliente</button>
    <button class="btn btn-primary" @click="getClients()" style="margin-left: 5px;"><i class="bi bi-arrow-clockwise"></i></button>

    <ClientModal ref="clientModal"/>
</template>

<script>
import axios from 'axios';
import ClientModal from "@/components/ClientModal.vue";

export default {
    data() {
        return {
            clients: []
        }
    },
    methods: {
        async getClients() {
            this.clients = [];
            const response = await axios.get("http://localhost:8080/crm/api/client");
            
            console.log(response);

            if (response.status === 200) {
                response.data.map(client => this.clients.push(client));
            }
        },
        openModalClient(client) {
            this.$refs.clientModal.showModal(client);
        }
    },
    beforeMount() {
        this.getClients();
    },
    components: {
        ClientModal
    }
}

</script>