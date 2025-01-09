<template>
    <div>
        <table>
            <thead>
                <tr>
                    <th></th>
                    <th>Fotografía</th>
                    <th>Título</th>
                    <th>Nombre</th>
                    <th>Apellido</th>
                    <th>Atributo 5 (Ciudad)</th>
                    <th>Atributo 6 (correo)</th>

                </tr>
            </thead>
            <tbody>
                <!--recorremos la lista de candidatos-->
                <tr v-for="(candidatos, index) in candidatos" :key="index">
                    <td>{{ index + 1 }}</td> <!--Para numerar candidatos-->
                    <td><img :src="candidatos.fotografia" alt="Fotografía" /></td>
                    <td>{{ candidatos.titulo }}</td>
                    <td>{{ candidatos.nombre }}</td>
                    <td>{{ candidatos.apellido }}</td>
                    <td>{{ candidatos.atributo5 }}</td>
                    <td>{{ candidatos.atributo6 }}</td>

                </tr>
            </tbody>
        </table>
    </div>
</template>

<script>
export default {
    props: {
        candidatos: {
            type: Array,
            required: true
        }
    }
};
</script>

<style scoped>
table {
    width: 100%;
    border-collapse: collapse;
    border: 2px solid blue;
    border-radius: 10px;
}

th,
td {
    border: 1px solid #ddd;
    padding: 8px;
}

th {
    background-color: #f2f2f2;
    text-align: left;
}
</style>