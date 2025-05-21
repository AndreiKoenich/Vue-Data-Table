<script setup>
import { ref } from 'vue';

const emit = defineEmits(['add-student']);

const newStudent = ref({
  nome: '',
  curso: '',
  media: ''
});

const submitForm = () => {
  if (newStudent.value.nome && newStudent.value.curso && newStudent.value.media) {
    emit('add-student', { ...newStudent.value });
    newStudent.value.nome = '';
    newStudent.value.curso = '';
    newStudent.value.media = '';
  }
};
</script>

<template>
  <form @submit.prevent="submitForm" style="margin-top: 20px;">
    <label>
      Nome:
      <input v-model="newStudent.nome" type="text" required />
    </label>
    <label>
      Curso:
      <input v-model="newStudent.curso" type="text" required />
    </label>
    <label>
      Média Total de Notas:
      <input v-model="newStudent.media" type="number" step="0.1" required />
    </label>
        <button type="submit">Adicionar</button>
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