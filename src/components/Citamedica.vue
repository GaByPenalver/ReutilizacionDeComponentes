<template>
<div class="container" :style="{backgroundColor:Gravedad}">
    <h3>Paciente</h3>
        <p>{{Paciente}}</p>
        <h3>Fecha</h3>
        <p>{{Fecha}}</p>
        <h3>Hora</h3>
        <p>{{Hora}}</p>
        <h3>Gravedad</h3>
        <p>{{Gravedad}}</p>
        <h3>Motivo</h3>
        <p>{{Motivo}}</p>
        <button @click="$emit('eliminarCita')">Eliminar</button>
</div>
</template>

<script>
export default {
    name: 'Citamedica',
    props:['Paciente','Fecha','Hora','Gravedad', 'Motivo']
}
</script>

<style scoped>

</style>