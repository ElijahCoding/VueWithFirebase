<template>
    <div id="dashboard">
        <h3>Dashboard</h3>

        <div class="fixed-action-btn">
            <router-link to="/new" class="btn btn-floating btn-large red">
                <i class="fa fa-plus"></i>
            </router-link>
        </div>
    </div>
</template>


<script>
    import db from './firebaseInit'

    export default {
        name: 'dashboard',

        data () {
            return {
                employees: []
            }
        },

        created () {
            db.collection('employees').get().then(querySnapShot => {
                querySnapShot.forEach(doc => {

                    const data = {
                        'id': doc.id,
                        'employee_id': doc.data().employee_id,
                        'name': doc.data().name,
                        'dept': doc.data().dept,
                        'position': doc.data().position
                    }
                    this.employees.push(data)
                })
            })
        }
    }
</script>
