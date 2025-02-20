<template>
    <table class="table table-hover table-bordered border-dark-subtle">
        <thead>
            <tr>
                <th>ID</th>
                <th>Primeiro Nome</th>
                <th>Último Nome</th>
                <th>E-mail</th>
            </tr>
        </thead>
        <tbody class="table-group-divider">
            <tr v-for="client in clients">
                <td>{{ client.id }}</td>
                <td>{{ client.firstName }}</td>
                <td>{{ client.lastName }}</td>
                <td>{{ client.email }}</td>
            </tr>
        </tbody>
        <div v-if="clients.length === 0" style="color: red; font-weight: bold;" class="">
            Sem dados
        </div>
    </table>
</template>

<script>
import axios from "axios"

export default {
    data() {
        return {
            clients: []
        }
    },
    methods: {
        async getClients() {
            const response = await axios.get("http://localhost:8080/crm/api/client");
            
            console.log(response);

            if (response.status === 200) {
                response.data.map(client => this.clients.push(client));
            }
        }
    },
    beforeMount() {
        this.getClients();
    }
}

</script>