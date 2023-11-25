<script setup>
import {ref, reactive} from "vue";
import Header from './components/Header.vue'
import Form from './components/Form.vue'

const paciente = reactive({
  nombre: '',
  propietario: '',
  email: '',
  alta: '',
  sintomas: '',
});

const pacientes = ref([]);

const savePaciente = () => {
  pacientes.value.push(paciente);
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
      />
      <div class="md:w-1/2 md:h-screen overflow-y-scroll ">
        <h3 class="font-black text-3xl text-center">Administra tus Pacientes</h3>
        <div v-if="pacientes.length > 0" class="">
        </div>
        <p v-else class="mt-10 text-2xl text-center">No Hay Pacientes</p>
      </div>
    </div>
  </div>
</template>
