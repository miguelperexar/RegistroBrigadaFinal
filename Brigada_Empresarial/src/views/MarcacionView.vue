<template>
    <div>
        <h4 align =center>{{ mensaje }}</h4>
        </div>
    <div class="col-md-6">
        <table class="table table-success table-striped">
            <thead>
                <tr>
                    <th>ID</th>
                    <th>TURNO</th>
                    <th>ENTRADA</th>
                    <th>SALIDA</th>
                    <th>PLANTA</th>
                    <th>FECHA</th>
                    <th>RANGO</th>

                </tr>
            </thead>
            <tbody>
                <!-- me recorre la lista-->
                <tr v-for="marcaciones in marcaciones">
                    <td>{{ marcaciones.id }}</td>
                    <td>{{ marcaciones.turno}}</td>
                    <td>{{ marcaciones.entrada }}</td>
                    <td>{{ marcaciones.salida}}</td>
                    <td>{{ marcaciones.planta }}</td>
                    <td>{{ marcaciones.fecha }}</td>
                    <td>{{ marcaciones.rango }}</td>
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
                <label for="Turno" class="form-label">Turno</label>
                <input v-model="turno" type="text" class="form-control" id="nombre" placeholder="Turno">
            </div>
            <div class="mb-3">
                <label for="Entrada" class="form-label">Entrada</label>
                <input v-model="entrada" type="text" class="form-control" id="Entrada" placeholder="Digite su Entrada">
            </div>
            <div class="mb-3">
                <label for="Salida" class="form-label">salida</label>
                <input v-model="salida" type="text" class="form-control" id="Salida" placeholder="digite su Salida">
            </div>
            <div class="mb-3">
                <label for="planta" class="form-label">Planta</label>
                <input v-model="planta" type="text" class="form-control" id="planta" placeholder="digite su planta">
            </div>
            <div class="mb-3">
                <label for="Fecha" class="form-label">Fecha</label>
                <input v-model="fecha" type="text" class="form-control" id="Fecha"
                    placeholder="Digite su digite la Fecha">
            </div>
            <div class="mb-3">
                <label for="años_brigadista" class="form-label">Rango</label>
                <input v-model="rango" type="text" class="form-control" id="Rango"
                    placeholder="Digite su digite su rango">
            </div>
            <div class="d-grid gap-2 d-md-block">
                <button type="button" class="btn btn-secondary" @click="crearbrigadistas">GUARDAR</button>
            <button type="button" class="btn btn-secondary" @click="">ACTUALIZAR</button>
            <button type="button" class="btn btn-secondary" @click="consultabrigadista">BUSCAR</button> 
            </div>
            
            
        </div>
    


</template>
<script>
export default {
    data() {
        return {
            mensaje: 'Localización de brigadistas',
            //codigo clase 3 miercoles lo hago con brigadistas
            //añado un metodo
            marcaciones: [],
            id: 0,
            turno: "",
            entrada: "",
            salida: "",
            planta: "",
            fecha: "",
            rango: ""
        };

    },
    methods: {
        //funcion para consultar
        limpiarDatos() {
            this.id = 0,
                this.turno = "",
                this.entrada = "",
                this.salida = "",
                this.planta = "",
                this.fecha = "",
                this.rango=""
        },
        async consultamarcaciones() {
            const opciones = {
                methods: 'GET',
                Headers: {
                    'Content-Type': 'application/json',
                    'Cache-Control': 'no-cache',
                    //la ruta se toma de postman
                    'Authorization': 'Basic dXNlcjpjMDhkZWIwYy01NjJhLTRiMzEtYjc1Yi1iZGMxZDMyMWY3MWY='
                }
            };
            //metodo javascrip
            fetch('http://localhost:8080/api/marcaciones', opciones)
                .then(async (response) => {
                    if (!response.ok) {
                        const error = new Error(response.statusText);
                        error.json = response.json();
                        console.log(error.message);
                        throw error;
                    }
                    else {
                        this.marcaciones = await response.json();
                        console.log(this.marcaciones);

                    }
                })
        },
        async crearmarcaciones() {
            const opciones = {
                methods: 'POST',
                Headers: {
                    'Content-Type': 'application/json',
                    'Cache-Control': 'no-cache',
                    //la ruta se toma de postman
                    'Authorization': 'Basic dXNlcjpjMDhkZWIwYy01NjJhLTRiMzEtYjc1Yi1iZGMxZDMyMWY3MWY='
                },
                body: JSON.stringify({
                    id: this.id,
                    turno: this.turno,
                    entrada: this.entrada,
                    salida: this.salida,
                    planta: this.planta,
                    fecha: this.fecha,
                    rango: this.rango

                })

            };
            fetch('http://localhost:8080/api/marcaciones', opciones)

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
                        this.consultamarcaciones();
                        this.limpiarDatos();
                    }
                });
        },
        async eliminarmarcacion(id) {
            const opciones = {
                methods: 'DELETE',
                Headers: {
                    'Content-Type': 'application/json',
                    'Cache-Control': 'no-cache',
                    //la ruta se toma de postman
                    'Authorization': 'Basic dXNlcjo0MjAxMTI2NS04M2U3LTQxN2YtYjg5Zi1jNWNkYmI5ODQ1OTU='
                }
            };
            //metodo javascrip
            fetch('http://localhost:8080/api/marcaciones/${id}', opciones)
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
                        this.consultamarcaciones();
                        this.limpiarDatos();
                    }
                })
        },
        eliminarconfmarcacion(id){
            if (!confirm('¡Esta segura de eliminar la marcación'))
            return;
            this.eliminarmarcacion(id);
        },
    },
    beforeMount() {
        this.consultamarcaciones();

    }

}

</script>
<style scoped>

</style>