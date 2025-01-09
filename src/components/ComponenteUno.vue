<template>
    <div class="container">
        <div class="formulario">
            <div class="container-formulario">
                <form>
                    <div class="fotografia">
                        <label for="Fotografia">Fotografía:</label>
                        <img :src="formularioDatos.fotografia" alt="Fotografía" v-if="formularioDatos.fotografia" />
                        <br>
                    </div>
                    <div class="informacion">
                        <label for="titulo">Título:</label>
                        <br>
                        <input type="text" id="titulo" v-model="formularioDatos.titulo"  />
                    </div>
                    <div class="informacion">
                        <label for="nombre">Nombre:</label>
                        <br>
                        <input type="text" id="nombre" v-model="formularioDatos.nombre"  />
                    </div>
                    <div class="informacion">
                        <label for="apellido">Apellido:</label>
                        <br>
                        <input type="text" id="apellido" v-model="formularioDatos.apellido"  />
                    </div>
                    <div class="informacion">
                        <label for="atributo5">Ciudad:</label>
                        <br>
                        <input type="text" id="atributo5" v-model="formularioDatos.atributo5"  />
                    </div>
                    <div class="informacion">
                        <label for="atributo6">Correo :</label>
                        <br>
                        <input type="email" id="atributo6" v-model="formularioDatos.atributo6"  />
                    </div>
                </form>
                <div class="container-botones">
                    <br>
                    <button @click="extraerData">Buscar</button>
                    <button @click="agregar">Agregar</button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            formularioDatos: { //arreglo con los datos del formulario
                fotografia: '',
                titulo: '',
                nombre: '',
                apellido: '',
                atributo5: '', //tomamos como atributo 5 la ciudad del json 
                atributo6: '' //tomamos como atributo 6 el correo del json 
            }
        };
    },
    methods: {
        async extraerData() { // metodo para consulta la api
            const urlApi = 'https://randomuser.me/api/';
            try {
                const respuestaApi = await fetch(urlApi);
                const data = await respuestaApi.json();
                const usuario = data.results[0]; //obtenemos el primer resultado de cada consulta

                this.formularioDatos = {
                    fotografia: usuario.picture.large,
                    titulo: usuario.name.title,
                    nombre: usuario.name.first,
                    apellido: usuario.name.last,
                    atributo5: usuario.location.city,
                    atributo6: usuario.email	
                };
            } catch (error) {
                console.error('Error:', error); //enviamos mensaje si no se puede consultar
            }
        },
        agregar() {
            this.$emit('aniadir-candidato', this.formularioDatos); // Emitimos el evento aniadir-candidato con la información del candidato
        }
    }
};
</script>

<style >
.container {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 70vh;
}

.formulario {
    display: flex;
    justify-content: center;
    align-items: center;
    border: 2px solid blue;
    border-radius: 10px;
    padding: 10px;
    height: 40vh;


}

.formulario label {
    color: blue;
    font-weight: bold;
    font-size: 20px
}

.formulario input {
    border: 1px solid rgb(128, 128, 131);
    border-radius: 3px;
    align-items: center;
    width: 175px;
    height: 20px;


}

.fotografia {
    display: flex;
    align-items: center;
}

.fotografia label {
    margin-right: 10px;
}

.fotografia img {
    width: 100px;
    height: 100px;
    border: 2px solid blue;
    border-radius: 10px;
}

.container-botones {
    display: flex;
    justify-content: space-between;
    margin-top: 10px;
}

button {
    background-color: blue;
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    margin: 7px;
    font-size: 20px;
    width: 80px;
}

button:hover{
    background-color: rgb(0, 217, 255);
    color: rgb(0, 6, 37);
}

.container-formulario {
    display: flex;
    flex-direction: column;
    align-items: center;
}
</style>