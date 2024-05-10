<script setup>
import { ref } from 'vue';
import AddStudentModal from './AddStudentModal.vue';

const students = ref([
    { id: 1, name: 'John Doe', email: 'johndoe@example.com', faculty: 'Faculty 1', year: '2022' },
    { id: 2, name: 'Jane Smith', email: 'janesmith@example.com', faculty: 'Faculty 2', year: '2023' },
    // Add more student data here if needed
]);

const showModal = ref(false);

const addStudent = (student) => {
    students.value.push({ ...student});
    showModal.value = false;
};

const cancelModal = () => {
    showModal.value = false;
};

const deleteStudent = (index) => {
    console.log(index)
    students.value.splice(index, 1);
};
</script>

<template>
    <div>
        <table>
            <thead>
                <tr>
                    <th>Name</th>
                    <th>Email</th>
                    <th>Faculty of Study</th>
                    <th>Year</th>
                    <th></th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="(student, index) in students" :key="index">
                    <td>{{ student.name }}</td>
                    <td>{{ student.email }}</td>
                    <td>{{ student.faculty }}</td>
                    <td>{{ student.year }}</td>
                    <td>
                        <button @click="deleteStudent(index)">X</button>
                    </td>
                </tr>
                <tr>
                    <td colspan="5">
                        <button @click="showModal = true">Add More Student +</button>
                    </td>
                </tr>
            </tbody>
        </table>

        <!-- Add Student Modal -->
        <AddStudentModal :showModal="showModal" @addStudent="addStudent" @cancelModal="cancelModal" />
    </div>
</template>

<style>
table {
    width: 80%;
    border-collapse: collapse;
}

thead th {
    background-color: #f2f2f2;
    border-bottom: 1px solid #ddd;
    padding: 8px;
    text-align: left;
}

tbody td {
    border-bottom: 1px solid #ddd;
    padding: 8px;
}

tbody tr:last-child td {
    text-align: center;
    font-weight: bold;
    cursor: pointer;
}

button {
    background-color: transparent;
    border: none;
    cursor: pointer;
}
</style>