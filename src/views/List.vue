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
                <td>
                    <button class="btn btn-secondary" @click="openModalClient(client)"><i class="bi bi-pencil-square"></i></button>
                    <button class="btn btn-danger" @click="deleteClient(client.id)" style="margin-left: 5px;"><i class="bi bi-trash3"></i></button>
                </td>
            </tr>
        </tbody>
        <div v-if="clients.length === 0" style="color: red; font-weight: bold;" class="">
            Sem dados
        </div>
    </table>

    <div>
        <button class="btn btn-secondary" @click="openModalClient(null)" style="float: left;">Criar Cliente</button>
        <button class="btn btn-success" style="float: right;" @click="exportToCsv"><i class="bi bi-file-earmark-spreadsheet"></i></button>
    </div>

    <ClientModal 
        ref="clientModal"
        :showToast="showToast"
        :listClient="getClients"
    />
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
    props: {
        showToast: Function
    },
    methods: {
        async getClients() {
            this.clients = [];
            const response = await axios.get("http://localhost:8080/crm/api/client")
                .catch(() => {
                    this.showToast("Ocorreu um erro ao buscar listagem", true);
                });
            
            console.log(response);

            if (response?.status === 200) {
                response.data.map(client => this.clients.push(client));
            } else {
                this.showToast("Ocorreu um erro ao buscar listagem", true);
            }
        },
        openModalClient(client) {
            this.$refs.clientModal.showModal(client);
        },
        deleteClient(id) {
            axios.delete("http://localhost:8080/crm/api/client/"+id)
                .then(() => {
                    this.showToast("Cliente apagado com sucesso", false);
                    this.getClients();
                });
        },
        exportToCsv() {
            axios.get("http://localhost:8080/crm/api/client/download")
                .then((response) => {
                    const blob = new Blob([response.data], { type: "text/plain" });
                    const link = document.createElement("a");
                    const url = URL.createObjectURL(blob);
                    link.href = url;
                    link.download = "example.csv";
                    document.body.appendChild(link);
                    link.click();
                    document.body.removeChild(link);
                    URL.revokeObjectURL(url);
                })
                .catch(() => {
                    this.showToast("Ocorreu um erro ao buscar ficheiro", true);
                });
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