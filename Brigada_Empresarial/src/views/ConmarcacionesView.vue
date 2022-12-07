<template>
    <div>
        <h4 align=center>buscador</h4>
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
                    <td>{{ marcaciones.turno }}</td>
                    <td>{{ marcaciones.entrada }}</td>
                    <td>{{ marcaciones.salida }}</td>
                    <td>{{ marcaciones.planta }}</td>
                    <td>{{ marcaciones.fecha }}</td>
                    <td>{{ marcaciones.rango }}</td>
                </tr>

            </tbody>
        </table>
    </div>
    <div class="col-md-6">

        <div class="mb-3">
            <label for="turno" class="form-label">Turno</label>
            <input v-model="turno" type="text" class="form-control" id="turno" placeholder="turno">
        </div>
        <div class="mb-3">
            <label for="entrada" class="form-label">Entrada</label>
            <input v-model="entrada" type="text" class="form-control" id="entrada" placeholder="Digite su Entrada">
        </div>
        <div class="d-grid gap-2">
            <button type="button" class="btn btn-secondary" @click="consultconamarcaciones(turno)">BUSCAR</button>
        </div>
    </div>
</template>
<script>
export default {
    data() {
        return {
            mensaje: 'Buscador de  brigadistas',
            //codigo clase 3 miercoles lo hago con brigadistas
            //añado un metodo
            conmarcaciones: [],
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

            this.turno = "",
                this.entrada = ""

        },
        async consultconamarcaciones(turno) {
            const opciones = {
                methods: 'GET',
                Headers: {
                    'Content-Type': 'application/json',
                    'Cache-Control': 'no-cache',
                    //la ruta se toma de postman
                    'Authorization': 'Basic dXNlcjo0MjAxMTI2NS04M2U3LTQxN2YtYjg5Zi1jNWNkYmI5ODQ1OTU='
                }
            };
            //metodo javascrip
            fetch('http://localhost:8080/api/marcaciones/turno', opciones)
                .then(async (response) => {
                    if (!response.ok) {
                        const error = new Error(response.statusText);
                        error.json = response.json();
                        console.log(error.message);
                        throw error;
                    }
                    else {
                        this.conmarcaciones = await response.json();
                        console.log(this.conmarcaciones);

                    }
                })
        },
        async consultaconamarcaciones() {
            const opciones = {
                methods: 'GET',
                Headers: {
                    'Content-Type': 'application/json',
                    'Cache-Control': 'no-cache',
                    //la ruta se toma de postman
                    'Authorization': 'Basic dXNlcjo0MjAxMTI2NS04M2U3LTQxN2YtYjg5Zi1jNWNkYmI5ODQ1OTU='
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
                        this.conmarcaciones = await response.json();
                        console.log(this.conmarcaciones);

                    }
                })
        }
    },
    beforeMount() {
        this.consultaconamarcaciones();

    }

}
</script>
<style scoped>

</style>