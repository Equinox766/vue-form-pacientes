<script setup>
import {ref, reactive} from "vue";
import { uid } from 'uid';
import Header from './components/Header.vue';
import Form from './components/Form.vue';
import Paciente from './components/Paciente.vue';

const paciente = reactive({
  id: null,
  nombre: '',
  propietario: '',
  email: '',
  alta: '',
  sintomas: '',
});

const pacientes = ref([]);

const savePaciente = () => {
  if (paciente.id) {
    const { id } = paciente;
    const i = pacientes.value.findIndex((pacienteState) => pacienteState.id === id)
    pacientes.value[i] = { ...paciente}
  } else {
    pacientes.value.push({
      ...paciente,
      id: uid()
    });
  }


  Object.assign(paciente, {
    nombre: '',
    propietario: '',
    email: '',
    alta: '',
    sintomas: '',
  })
}

const updatePaciente = (id) => {
  const pacienteEdit = pacientes.value.filter(paciente => paciente.id === id)[0]
  Object.assign(paciente, pacienteEdit)
}
</script>

<template>
  <div class="container mx-auto mt-20">
    <Header/>
    <div class="mt-12 md:flex ">
      <Form
          v-model:nombre="paciente.nombre"
          v-model:propietario="paciente.propietario"
          v-model:email="paciente.email"
          v-model:alta="paciente.alta"
          v-model:sintomas="paciente.sintomas"
          @save-paciente="savePaciente"
          :id="paciente.id"
      />
      <div class="md:w-1/2 md:h-screen overflow-y-scroll ">
        <h3 class="font-black text-3xl text-center">Administra tus Pacientes</h3>
        <div v-if="pacientes.length > 0" class="">
          <p class="text-lg mt-5 text-center mb-10">
            Información de
            <span class="text-indigo-600 font-bold">Pacientes</span>
          </p>
          <Paciente
            v-for="paciente in pacientes"
            :paciente="paciente"
            @update-paciente="updatePaciente"
          />
        </div>
        <p v-else class="mt-10 text-2xl text-center">No Hay Pacientes</p>
      </div>
    </div>
  </div>
</template>
