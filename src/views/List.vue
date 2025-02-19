<template>
    <table class="table">
        <thead>
            <tr>
                <th>ID</th>
                <th>Primeiro Nome</th>
                <th>Último Nome</th>
                <th>E-mail</th>
            </tr>
        </thead>
        <tbody v-for="client in getClients()">
            <tr>
                <td>{{ client.id }}</td>
                <td>{{ client.firstName }}</td>
                <td>{{ client.lastName }}</td>
                <td>{{ client.email }}</td>
            </tr>
        </tbody>
        <div v-if="getClients().length === 0" style="color: red; font-weight: bold;">
            Sem dados
        </div>
    </table>
</template>

<script>
export default {
    methods: {
        getClients() {
            return [{id: 1, firstName: "rui", lastName: "andrade", email: "test@test.com"}]
        }
    }
}

</script>