<template>
    <div>
        <b-modal id="deleteStudentModal" title="Delete Student" ok-title="Delete Student" @ok="onDelete" ok-variant="danger">
            Are you sure in deleting this student? <br><br>
            Name: {{student.name}} <br>
            Age: {{student.age}}
        </b-modal>
    </div>
</template>

<script>
export default {
    props: {
        student: {}
    },
    methods: {
        async onDelete() {
            this.$axios.delete('/api/students/' + this.student.id)
            .then((res)=>{
                if(res.status==202) {
                    alert('Deleted successfully!')
                    this.$emit('onDeleted')
                }
            })
        }
    }
}
</script>