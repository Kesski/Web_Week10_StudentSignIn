<template>
    <div>
        <!-- Template/HTML here -->
        <div v-if="student.name">
            <div class="alert alert-success" v-if="mostRecentStudent.present">
                Welcome, {{ mostRecentStudent.name }}
            </div>

            <div class="alert alert-info" v-else>
                Goodbye, {{ student.name }}. See you later.
            </div>

        </div>
    </div>
</template>

<script>
    export default {
        name: 'StudentMessage',
        props: {
            student: Object
        }
    }

</script>

<style scoped>

</style>