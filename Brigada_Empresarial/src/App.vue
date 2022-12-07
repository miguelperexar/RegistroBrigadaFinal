<template>
    <div class="container">
        <div class="row">
            <div class="col-md-12">
                <Encabezado />
            </div>
        </div >
       <nav class="navbar navbar-expand-lg bg-warning" ms-auto>
        <div class="row">
            <!--estas clases son de bootstrap-->
            <ul class="nav">
                <li class="nav-item">
                    <!--RouterLink nos permite acceder a path ingresados anteriormente al router-->
                    <RouterLink class="nav-link" to="/"> Inicio</RouterLink>
                </li>
                <li class="nav-item">
                    <RouterLink class="nav-link" to="/brigadistas"> Brigadistas</RouterLink>
                </li>
                <li class="nav-item">
                    <RouterLink class="nav-link" to="/marcacion"> Marcacion</RouterLink>
                </li>
                <li class="nav-item">
                    <RouterLink class="nav-link" to="/conmarcaciones"> Registro diario</RouterLink>
                </li>
            </ul>
        </div>
    </nav>
        <div class="row contenido">
            <RouterView />
        </div>
        <div class="row">
            <div class="col-md-12">
                <Pie v-model:token="token" />
            </div>
        </div>
    </div>
</template>
<script>
import { RouterLink, RouterView } from 'vue-router'
import Encabezado from './components/Encabezado.vue';
import Pie from './components/Pie.vue';

export default {
    data() {
        return {
            token: 'pendiente',
            brigadistas: '/brigadistas',
            marcacion: '/marcacion',
            conmarcaciones: '/conmarcaciones'
        };
    },
    components: { Encabezado, Pie }
}
</script>

<style scoped>
.contenido {
    padding: 12px;
    border: 1px solid #ccc;
    border-radius: 8px;
    min-height: 550px;
}
</style>
    