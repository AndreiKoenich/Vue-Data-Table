<script setup>
defineProps({
  students: {
    type: Array,
    required: true
  }
});

const emit = defineEmits(['remove-student', 'show-update-student-form']);

const headers = [
  { title: 'Nome', key: 'nome' },
  { title: 'Curso', key: 'curso' },
  { title: 'Média Total de Notas', key: 'media' },
  { title: 'Remoção', key: 'remocao', sortable: false },
  { title: 'Atualização', key: 'atualizacao', sortable: false }
];
</script>

<template>
  <v-container>
    <v-data-table
      :headers="headers"
      :items="students"
      :no-data-text="'Nenhum estudante encontrado.'"
      item-value="index"
      class="elevation-1"
      hide-default-footer
    >
      <template #top>
        <h3 class="text-h5 text-center">Lista de Estudantes</h3>
      </template>
      <template #item.remocao="{ item, index }">
        <v-btn color="red" @click="emit('remove-student', index)">Remover</v-btn>
      </template>
      <template #item.atualizacao="{ item, index }">
        <v-btn color="blue" @click="emit('show-update-student-form', index)">Atualizar</v-btn>
      </template>
    </v-data-table>
  </v-container>
</template>