<script setup>
import { reactive } from "vue";
import Alert from './Alert.vue';

const alert = reactive({
  type: '',
  msg: ''
})

const props = defineProps({
  nombre:{
    type: Object,
    required: true
  },
  propietario:{
    type: Object,
    required: true
  },
  alta:{
    type: Object,
    required: true
  },
  email:{
    type: Object,
    required: true
  },
  sintomas:{
    type: Object,
    required: true
  },
})

const emit = defineEmits(['update:nombre', 'update:propietario', 'update:email', 'update:alta', 'update:sintomas', 'save-paciente'])
const validar = () => {
  if (Object.values(props).includes('')) {
    alert.msg = 'Todos los campos son obligatorios';
    alert.type = 'error';
    return
  }

  emit('save-paciente')
}
</script>

<template>
  <div class="md:w-1/2">
    <h2 class="font-black text-3xl text-center">Seguimiento Pacientes</h2>
    <p class="text-lg mt-5 text-center mb-10">
      Añade pacientes y
      <span class="text-indigo-600 font-bold">Adminístralos</span>
    </p>

    <Alert
        v-if="alert.msg"
        :alert="alert"
    />

    <form action="" class="bg-white shadow-md rounded-lg py-10 px-5 mb-10" @submit.prevent="validar">
      <div class="mb-5">
        <label for="mascota" class="block text-gray-700 uppercase font-bold">
          Nombre Mascota:
        </label>
        <input type="text" id="mascota" placeholder="Nombre de la mascota"
               class="border-2 w-full p-2 placeholder-gray-400 rounded-md" @input="$emit('update:nombre', $event.target.value)">
      </div>
      <div class="mb-5">
        <label for="propietario" class="block text-gray-700 uppercase font-bold">
          Nombre del Propietario:
        </label>
        <input type="text" id="propietario" placeholder="Nombre del Propietario"
               class="border-2 w-full p-2 placeholder-gray-400 rounded-md" @input="$emit('update:propietario', $event.target.value)">
      </div>
      <div class="mb-5">
        <label for="email" class="block text-gray-700 uppercase font-bold">
          Email del Propietario:
        </label>
        <input type="email" id="email" placeholder="Email del Propietario"
               class="border-2 w-full p-2 placeholder-gray-400 rounded-md" @input="$emit('update:email', $event.target.value)">
      </div>
      <div class="mb-5">
        <label for="alta" class="block text-gray-700 uppercase font-bold">
          Alta del Propietario:
        </label>
        <input type="date" id="alta" class="border-2 w-full p-2 placeholder-gray-400 rounded-md"
               @input="$emit('update:alta', $event.target.value)">
      </div>
      <div class="mb-5">
        <label for="sintomas" class="block text-gray-700 uppercase font-bold">
          Sintomas:
        </label>
        <textarea
            id="sintomas"
            placeholder="Describe los síntomas"
            class="border-2 w-full p-2 placeholder-gray-400 rounded-md h-40"
            @input="$emit('update:sintomas', $event.target.value)"
        />
      </div>
      <input type="submit"
             class="bg-indigo-600 w-full text-white uppercase font-bold hover:bg-indigo-800 cursor-pointer transition-colors p-3"
             value="Registrar Paciente">
    </form>
  </div>
</template>