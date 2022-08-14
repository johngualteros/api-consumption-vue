<!-- eslint-disable vue/multi-word-component-names -->
<template>
    <div class="container">
        <form class="card card-body" v-on:submit.prevent="addEmployee">
            <h1>Add Employee</h1>
            <div class="mb-3">
                <label for="name">Name</label>
                <input type="text" class="form-control" id="name" v-model="employee.name" placeholder="Name">
            </div>
            <div class="mb-3">
                <label for="email">Email</label>
                <input type="email" class="form-control" id="email" v-model="employee.email" placeholder="Email">
            </div>
            <button class="btn btn-primary my-2 fw-bold" type="submit">Add</button>
            <router-link :to="{name:'list'}" class="btn btn-danger my-2 fw-bold" >Cancel</router-link>
        </form>
    </div>
</template>

<script>
export default{
    data(){
        return{
            employee:{
                name:'',
                email:''
            }
        }
    },
    methods: {
        addEmploye(){
            var newEmployee = {
                name: this.employee.name,
                email: this.employee.email
            }
            fetch('http://localhost/empleados/?insertar=1',{
                method:'POST',
                body:JSON.stringify(newEmployee)
            }).then((response=>{
                console.log(response);
                window.location.href="list"
            }))
        }
    },
}
</script>