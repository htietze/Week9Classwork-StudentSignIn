<template>

    <div class="card student-list m-2 p-2">
        <h4 class="card-title">Students</h4>

        <div class="edit-table-toggle form-check">
            <input id="edit-table" type="checkbox" class="form-check-input" v-model="editTable">
            <label for="edit-table" class="form-check-label">Edit table?</label>
        </div>

        <div id="student-table">
            <table class="table">
                <tr>
                    <th>Name</th>
                    <th>StarID</th>
                    <th>Present?</th>
                    <th v-show="editTable">Delete</th>
                </tr>
                <StudentRow
                    v-for="student in students" v-bind:key="student.name"
                    v-bind:student="student"
                    v-bind:edit="editTable"
                    v-on:student-Present="studentArrivedOrLeft"
                    v-on:delete-student="studentDeleted">
                </StudentRow>

                    <!-- OLD CODE:
                        <tr class="student-row" v-for="student in students" v-bind:key="student.name" v-bind:class="'present-'+student.present">
                        <td>{{student.name}}</td>
                        <td>{{student.starID}}</td>
                        <td><input type='checkbox' 
                        v-on:change='checked(student)' v-model='student.present'></td>
                    </tr> -->
            </table>
        </div>
    </div>

</template>

<script>

    import StudentRow from '@/components/StudentRow.vue'
    
    export default {
        name: 'StudentTable',
        components: { StudentRow },
        data() {
            return {
                editTable: false
            }
        },
        props: {
            students: Array
        },
        methods: {
            studentArrivedOrLeft(student) {
                this.$emit('student-present', student)
            },
            studentDeleted(student) {
                this.$emit('delete-student', student)
            }
        }
    }

</script>

<style>

.present-true {
    color: gray;
    font-style: italic;
}

.present-false {
    font-weight: bold;
}

</style>