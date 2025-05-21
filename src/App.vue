<script setup>
import { ref } from 'vue';
import StudentsTable from './components/StudentsTable.vue';
import AddStudentForm from './components/CreateStudentForm.vue';
import UpdateStudentForm from './components/UpdateStudentForm.vue';

const students = ref([])
let studentToUpdateIndex = ref(null)
const studentToUpdate = ref(null);
const isUpdating = ref(false);

const showUpdateStudentForm = (index) => {
    isUpdating.value = true;
    studentToUpdateIndex.value = index;
    studentToUpdate.value = { ...students.value[index] }; 
};

const updateStudent = (updatedStudent) => {
  students.value[studentToUpdateIndex.value] = updatedStudent;
  studentToUpdateIndex.value = null;
  isUpdating.value = false;
};

const addStudent = (student) => {
  students.value.push(student);
};

const removeStudent = (index) => {
  students.value.splice(index, 1);
};
</script>

<template>
  <div>
    <StudentsTable :students="students" @remove-student="removeStudent" @show-update-student-form="showUpdateStudentForm"/>
    <div v-if="isUpdating">
      <UpdateStudentForm :student="studentToUpdate" @update-student="updateStudent"/>
    </div>
    <div v-else>
      <AddStudentForm @add-student="addStudent"/>
    </div>
  </div>
</template>