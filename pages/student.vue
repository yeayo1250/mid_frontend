<template>
    <div>
        <NavBar />
        <EditStudentModal :student="selectedStudent" />
        <DeleteStudentModal :student="selectedStudent" @onDeleted="getAll" />

        <div class="container">
            <h1>
                LIST OF STUDENT
            </h1>
            
            <StudentEntryModal class="float-right mb-1" @onAdd="getAll" />

            <table class="table table-bordered table-striped table-primary">
                <thead>
                    <tr class="bg-info text-white">
                        <th>Name</th>
                        <th>Address</th>
                        <th>Age</th>
                        <th>Date Enrolled</th>
                        <th>Gender</th>
                        <th>&nbsp;</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="student in students" :key="student.id">
                        <td>{{student.name}}</td>
                        <td>{{student.address}}</td>
                        <td>{{student.age}}</td>
                        <td>{{student.date_enrolled}}</td>
                        <td>{{student.gender}}</td>
                        <td class="buttons">
                            <b-button @click="onEdit(student)" variant="primary" size="sm">
                                Edit
                            </b-button>
                            <b-button @click="onDelete(student)" variant="danger" size="sm">
                                Delete
                            </b-button>
                        </td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
           students: [],
            selectedStudent: {}
        }
    },
    methods: {
        async getAll() {
            await this.$axios.get('/api/students')
            .then((res)=>{
                if (res.status==200) {
                    this.students = res.data
                };
            })
        },
        onEdit(selectedStudent) {
            this.selectedStudent = selectedStudent
            this.$bvModal.show('editStudentModal')
        },
        onDelete(selectedStudent) {
            this.selectedStudent = selectedStudent
            this.$bvModal.show('deleteStudentModal')
        }
    },
    created() {
        this.getAll()
    }
}
</script>

<style>
h1 {
    text-align: center;
    margin-top: 50px;
}
.buttons {
    text-align: center;
}
</style>