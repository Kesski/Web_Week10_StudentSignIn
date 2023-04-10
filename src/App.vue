<template>
  <div id="app">

    <new-student-form>v-on:student-added="newStudentAdded"></new-student-form>
    <student-message v-bind:student="mostRecentStudent"></student-message>
    <student-table 
    v-bind:students="students" 
    v-on:students-arrived-or-left="studentsArrivedOrLeft"
    v-on:delete-student="studentDeleted">
    </student-table>
  </div>
</template>

<script>
import NewStudentForm from './components/NewStudentForm.vue'
import StudentMessage from './components/StudentMessage.vue'
import StudentTable from './components/StudentTable.vue'

export default {
  name: 'App',
  components: {
    NewStudentForm,
    StudentMessage,
    StudentTable
  },
  data() {
    return {
      students: [],
      mostRecentStudent: {}
    }
  },
  methods: {
    newStudentAdded(student) {
      this.students.push(student)
      this.students.sort(function(s1, s2) {
        return s1.name.toLowerCase() < s2.name.toLowerCase() ? -1 : 1
      })
    },
    studentsArrivedOrLeft(student, present) {
      // find student in array of students
      //update present attribute

      let updateStudent = this.students.find( function(s) {
        if(s.name === student.name && s.starID === student.starID) {
          return true // this is the student to update
        }
      })
      if (updateStudent) {
        updateStudent.present = present
        this.mostRecentStudent = updateStudent
      }
    },
    studentDeleted(student) {
      // filter returns new array of all students for whom the function returns true
      this.students = this.students.filter( function(s) {
        if (s != student) {
          return true
        }
      })

      this.mostRecentStudent = {} // clear welcome message
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

@import "https://cdn.jsdelivr.net/npm/bootstrap@4.6.0/dist/css/bootstrap.min.css";
</style>
