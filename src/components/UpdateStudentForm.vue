<script setup>
import { ref, onMounted } from 'vue';

const props = defineProps({
  student: {
    type: Object,
    required: true
  }
});

const emit = defineEmits(['update-student']);

const updatedStudent = ref({
  nome: '',
  curso: '',
  media: ''
});

onMounted(() => {
  updatedStudent.value = { ...props.student };
});

const submitForm = () => {
  if (updatedStudent.value.nome && updatedStudent.value.curso && updatedStudent.value.media) {
    emit('update-student', { ...updatedStudent.value });
  }
};
</script>

<template>
  <form @submit.prevent="submitForm" style="margin-top: 20px;">
    <label>
      Nome:
      <input v-model="updatedStudent.nome" type="text" required />
    </label>
    <label>
      Curso:
      <input v-model="updatedStudent.curso" type="text" required />
    </label>
    <label>
      Média Total de Notas:
      <input v-model="updatedStudent.media" type="number" step="0.1" required />
    </label>
    <button type="submit">Atualizar</button>
  </form>
</template>

<style scoped>
form {
    display: flex;
    flex-direction: column;
    gap: 10px;
}

label {
    display: flex;
    text-align: center;
    flex-direction: column;
}

input {
    width: 500px; 
    padding: 5px; 
    margin: 5px auto; 
    border: 1px solid black; 

}

button {
    text-align: center;
    align-self: center;
    width: 300px; 
    border: 1px solid black; 
    border-radius: 4px; 
}

</style>