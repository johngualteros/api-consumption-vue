<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <div class="container">
    <div class="card card-body">
      <table class="table">
        <thead class="text-center">
          <tr>
            <th>#</th>
            <th>Name</th>
            <th>Email</th>
            <th>Action</th>
          </tr>
        </thead>
        <tbody class="text-center">
          <tr v-for="employee in employees" v-bind:key="employee.id">
            <td>{{ employee.id }}</td>
            <td>{{ employee.name }}</td>
            <td>{{ employee.email }}</td>
            <td>
              <router-link :to="{name:'edit',params:{id:employee.id}}" class="btn btn-sucess m-1"
                >Edit</router-link
              >
              |
              <button class="btn btn-danger m-1" v-on="deleteEmployee(employee.id)" 
                >Delete</button
              >
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
      employees: [],
    };
  },
  methods: {
    consultEmployees() {
      fetch("https://localhost/empleados/")
        .then((response) => response.json())
        .then((data) => {
          this.employees = data;
        })
        .catch((error) => {
          console.log(error);
        });
    },
    deleteEmployee(id){
        fetch(`https://localhost/empleados/?borrar=${id}`,{
            method:'DELETE'
        }).then((res)=>{
            console.log(res);
            this.consultEmployees();
        }).catch((error)=>{
            console.log(error);
        })
    }
  },
  mounted() {
    this.consultEmployees();
  },
};
</script>
