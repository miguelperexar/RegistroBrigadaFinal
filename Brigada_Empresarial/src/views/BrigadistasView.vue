<template>
    <div>
        <h4 align=center>{{ mensaje }}

        </h4>
    </div>
    <div class="col-md-6">
        <table class="table table-success table-sm" align=center>
            <thead>
                <tr>
                    <th>ID</th>
                    <th>NOMBRE</th>
                    <th>APELLIDO</th>
                    <th>DIRECCION</th>
                    <th>PLANTA</th>
                    <th>AÑOS_BRIGADISTA</th>

                </tr>
            </thead>
            <tbody>
                <!-- me recorre la lista-->
                <tr v-for="brigadista in brigadistas">
                    <td>{{ brigadista.id }}</td>
                    <td>{{ brigadista.nombre }}</td>
                    <td>{{ brigadista.apellido }}</td>
                    <td>{{ brigadista.direccion }}</td>
                    <td>{{ brigadista.planta }}</td>
                    <td>{{ brigadista.años_brigadista }}</td>
                </tr>

            </tbody>
        </table>
    </div>
    <div class="col-md-6">
        <div class="mb-3">
            <label for="id" class="form-label">Cédula</label>
            <input v-model="id" type="number" class="form-control" id="id" placeholder="digite su cédula">
        </div>
        <div class="mb-3">
            <label for="nombre" class="form-label">Nombre</label>
            <input v-model="nombre" type="text" class="form-control" id="nombre" placeholder="digite su nombre">
        </div>
        <div class="mb-3">
            <label for="apellido" class="form-label">Apellido</label>
            <input v-model="apellido" type="text" class="form-control" id="apellido" placeholder="digite su apellido">
        </div>
        <div class="mb-3">
            <label for="direccion" class="form-label">direccion</label>
            <input v-model="direccion" type="text" class="form-control" id="direccion"
                placeholder="digite su direccion">
        </div>
        <div class="mb-3">
            <label for="planta" class="form-label">Planta</label>
            <input v-model="planta" type="text" class="form-control" id="planta" placeholder="digite su planta">
        </div>
        <div class="mb-3">
            <label for="años_brigadista" class="form-label">Años que lleva en brigada</label>
            <input v-model="años_brigadista" type="number" class="form-control" id="años_brigadista"
                placeholder="digite su digite los años en brigada">
        </div>
        <div class="d-grid gap-2 d-md-block">
            <button type="button" class="btn btn-danger" @click="crearbrigadistas">GUARDAR</button>
            <button type="button" class="btn btn-danger" @click="">ACTUALIZAR</button>
            <button type="button" class="btn btn-danger" @click="consultabrigadista">BUSCAR</button>
            <button type="button" class="btn btn-danger" @click="eliminarbrigadista(id)">ELIMINAR</button>
        </div>

    </div>



</template>
<script>
export default {
    data() {
        return {
            mensaje: 'Bienvenidos administradores del sistema',
            //codigo clase 3 miercoles lo hago con brigadistas
            //añado un metodo
            brigadistas: [],
            id: 0,
            nombre: "",
            apellido: "",
            direccion: "",
            planta: "",
            años_brigadista: 0
        };

    },
    methods: {
        //funcion para consultar
        limpiarDatos() {
            this.id = 0,
                this.nombre = "",
                this.apellido = "",
                this.direccion = "",
                this.planta = "",
                this.años_brigadista = 0
        },
        async consultabrigadista() {
            const opciones = {
                methods: 'GET',
                Headers: {
                    'Content-Type': 'application/json',
                    'Cache-Control': 'no-cache',
                    //la ruta se toma de postman
                    'Authorization': 'Basic dXNlcjozNjk2YTIzMi05MWI5LTQ4NTktOTA5Mi0zMmFlYjQyY2ExZDU='

                }
            };
            //metodo javascrip
            fetch('http://localhost:8080/api/brigadistas', opciones)
                .then(async (response) => {
                    if (!response.ok) {
                        const error = new Error(response.statusText);
                        error.json = response.json();
                        console.log(error.message);
                        throw error;
                    }
                    else {
                        this.brigadistas = await response.json();
                        console.log(this.brigadistas);

                    }
                })
        },
        async crearbrigadistas() {
            const opciones = {
                methods: 'POST',
                Headers: {
                    'Content-Type': 'application/json',
                    'Cache-Control': 'no-cache',
                    //la ruta se toma de postman
                    'Authorization': 'Basic dXNlcjozNjk2YTIzMi05MWI5LTQ4NTktOTA5Mi0zMmFlYjQyY2ExZDU='
                },
                body: JSON.stringify({
                    id: this.id,
                    nombre: this.nombre,
                    apellido: this.apellido,
                    direccion: this.direccion,
                    planta: this.planta,
                    años_brigadista: this.años_brigadista

                })

            };
            fetch('http://localhost:8080/api/brigadistas', opciones)

                //fetch('http://localhost:8080/api/brigadistas', opciones)
                .then(async (response) => {
                    if (!response.ok) {
                        const error = new Error(response.statusText);
                        error.json = response.json();
                        console.log(error.message);
                        throw error;
                    }
                    else {

                        const data = await response.json();
                        console.log(data);
                        this.consultabrigadista();
                        this.limpiarDatos();
                    }
                });
        },
        async eliminarbrigadista(id) {
            const opciones = {
                methods: 'DELETE',
                Headers: {
                    'Content-Type': 'application/json',
                    'Cache-Control': 'no-cache',
                    //la ruta se toma de postman
                    'Authorization': 'Basic dXNlcjozNjk2YTIzMi05MWI5LTQ4NTktOTA5Mi0zMmFlYjQyY2ExZDU='
                }
            };
            //metodo javascrip
            fetch('http://localhost:8080/api/brigadistas/${id}', opciones)
                .then(async (response) => {
                    if (!response.ok) {
                        const error = new Error(response.statusText);
                        error.json = response.json();
                        console.log(error.message);
                        throw error;
                    }
                    else {
                        this.brigadistas = await response.json();
                        console.log(data);
                        this.consultabrigadista();
                        this.limpiarDatos();
                    }
                })
        },
        eliminarconftarea(id) {
            if (!confirm('¡Esta segura de eliminar el regsitro'))
                return;
            this.eliminarbrigadista(id);
        },
    },
    beforeMount() {
        this.consultabrigadista();

    }

}

</script>
<style scoped>

</style>