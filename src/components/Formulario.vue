<template>
    <div class="container">
    <div class="form">
        <div class="labels">

        <div class="info">
        <label :style="{ color: Paciente ? 'black' : 'red' }"><strong>Paciente </strong></label>
        <input type="text" v-model="Paciente" />
        </div>

        <div class="info">
        <label :style="{ color: Fecha ? 'black' : 'red' }"><strong>Fecha </strong></label>
        <input type="date" v-model="Fecha" />
        </div>
        <div class="info">
        <label :style="{ color: Hora ? 'black' : 'red' }"><strong>Hora </strong></label>
        <input type="time" v-model="Hora" />
        </div>
        <div class="info">
        <label :style="{ color: Gravedad ? 'black' : 'red' }"><strong>Gravedad </strong></label>
        <select v-model="Gravedad" id="Gravedad">
            <option value="" disabled></option>
            <option value="green">Baja</option>
            <option value="yellow">Media</option>
            <option value="red">Alta</option>
        </select>
        </div>
        <div class="info">
        <label :style="{ color: Motivo ? 'black' : 'red' }"><strong>Motivo </strong></label>
        <input type="text" v-model="Motivo" />
        </div>
    </div>
    <div class="button-container">
        <button
        @click="agregarCita"
        :disabled="!Paciente || !Fecha || !Hora || !Gravedad || !Motivo"
        >
        Agregar
        </button>
    </div>
        
    </div>

    <section class="cita">
        <Citamedica
        v-for="(cita, index) in citas"
        :key="index"
        :Paciente="cita.Paciente"
        :Fecha="cita.Fecha"
        :Hora="cita.Hora"
        :Gravedad="cita.Gravedad"
        :Motivo="cita.Motivo"
        @eliminarCita="citas.splice(index, 1)"
        />
    </section>

    <div v-if="citas.length === 0" class="alert">
            <p style="color: red;">Aún no hay consultas registradas</p>
        </div>
    </div>

</template>

<script>
import Citamedica from "./Citamedica.vue";

export default {
name: "Formulario",
components: {
    Citamedica,
},
data() {
    return {
    Paciente: "",
    Fecha: "",
    Hora: "",
    Gravedad: "",
    Motivo: "",
    citas: [],
    };
},
methods: {
    agregarCita() {
    if (
        this.Paciente &&
        this.Fecha &&
        this.Hora &&
        this.Gravedad &&
        this.Motivo
    ) {
        this.citas.push({
        Paciente: this.Paciente,
        Fecha: this.Fecha,
        Hora: this.Hora,
        Gravedad: this.Gravedad,
        Motivo: this.Motivo,
        });

        this.Paciente = "";
        this.Fecha = "";
        this.Hora = "";
        this.Gravedad = "";
        this.Motivo = "";
    }
    },
},
};
</script>

<style scoped>
.container {
display: flex;
flex-direction: column;
align-items: center;
width: 100%;
}

.form {
display: flex;
flex-direction: column;
gap: 1rem;
border: 1px solid #000;
padding: 50px;
margin-top: 20px;
}
.labels {
display: flex;
gap: 1rem;
}
.button-container {
margin-top: 1rem;
text-align: center;
}

.cita {
display: flex;
flex-direction: row;
gap: 10px;
justify-content: center;
width: 15%;
margin: 0 auto;
}

.info {
display: flex;
flex-direction: column;
align-items: center;
}
</style>
