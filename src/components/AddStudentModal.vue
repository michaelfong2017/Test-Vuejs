<script setup>
import { ref, defineProps, defineEmits } from 'vue';

defineProps(['showModal']);
const emit = defineEmits(['addStudent', 'cancelModal']);

const faculties = [
    'Faculty of Architecture',
    'Faculty of Arts',
    'Faculty of Business and Economics (HKU Business School)',
    'Faculty of Dentistry',
    'Faculty of Education',
    'Faculty of Engineering',
    'Faculty of Law',
    'Li Ka Shing Faculty of Medicine',
    'Faculty of Science',
    'Faculty of Social Sciences'
];

const newStudent = ref({ name: '', email: '', faculty: '', year: '' });

const submitForm = () => {
    if (newStudent.value.name !== '' && newStudent.value.email !== '' && newStudent.value.faculty !== '' && newStudent.value.year !== '') {
        emit('addStudent', { ...newStudent.value });
        newStudent.value = { name: '', email: '', faculty: '', year: '' };
    }
};

const cancelModal = () => {
  emit('cancelModal');
};

</script>

<template>
    <div class="modal" v-if="showModal">
        <div class="modal-content">
            <h2>Add Student</h2>
            <form @submit.prevent="submitForm">
                <div class="form-group">
                    <label for="name">Name:</label>
                    <input id="name" v-model="newStudent.name" type="text" placeholder="Enter student name" />
                </div>
                <div class="form-group">
                    <label for="email">Email:</label>
                    <input id="email" v-model="newStudent.email" type="text" placeholder="Enter student email" />
                </div>
                <div class="form-group">
                    <label for="faculty">Faculty:</label>
                    <select id="faculty" v-model="newStudent.faculty">
                        <option value="">Select faculty</option>
                        <option v-for="faculty in faculties" :key="faculty" :value="faculty">{{ faculty }}</option>
                    </select>
                </div>
                <div class="form-group">
                    <label for="year">Year:</label>
                    <input id="year" v-model="newStudent.year" type="text" placeholder="Enter student year" />
                </div>
                <div>
                    <button type="submit" style="margin-right: 10px;">Submit</button>
                    <button type="button" @click="cancelModal">Cancel</button>
                </div>
            </form>
        </div>
    </div>
</template>

<style scoped>
.modal {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.5);
    display: flex;
    justify-content: center;
    align-items: center;
}

.modal-content {
    background-color: white;
    padding: 20px;
    border-radius: 5px;
    width: 80%;
    /* Adjust the width as needed */
    max-width: 500px;
    /* Optional: Set a maximum width for the modal */
    box-sizing: border-box;
}

.form-group {
    margin-bottom: 10px;
}

label {
    display: block;
}

input,
select {
    border: none;
    border-bottom: 1px solid #ccc;
    padding: 5px;
    width: 100%;
}

button {
    background-color: #007bff;
    color: white;
    border: none;
    padding: 5px 10px;
    border-radius: 5px;
    cursor: pointer;
}

button:focus {
    outline: none;
}

button:active {
    background-color: #0056b3;
}
</style>