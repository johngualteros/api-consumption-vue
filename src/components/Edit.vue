<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <div class="container">
    <form class="card card-body" v-on:submit.prevent="updateEmployee">
      <h1>update Employee</h1>
      <div class="mb-3">
        <label for="name">Name</label>
        <input
          type="text"
          class="form-control"
          id="name"
          v-model="employee.name"
          placeholder="Name"
        />
      </div>
      <div class="mb-3">
        <label for="email">Email</label>
        <input
          type="email"
          class="form-control"
          id="email"
          v-model="employee.email"
          placeholder="Email"
        />
      </div>
      <button class="btn btn-primary my-2 fw-bold" type="submit">Update</button>
      <router-link :to="{ name: 'list' }" class="btn btn-danger my-2 fw-bold"
        >Cancel</router-link
      >
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      employee: {},
    };
  },
  method: {
    consultEmployees() {
      fetch("https://localhost/empleados/?consultar="+this.route.params.id)
        .then((response) => response.json())
        .then((data) => {
          this.employee = data[0];
        })
        .catch((error) => {
          console.log(error);
        });
    },
    updateEmployee(){
        var newEmployee = {
            id: this.route.params.id,
            name: this.employee.name,
            email: this.employee.email
        }
        fetch("https://localhost/empleados/?actualizar="+this.route.params.id,{
            method:'POST',
            body:JSON.stringify(newEmployee)
        }).then((response=>{
            console.log(response);
            window.location.href="../list"
        }))
    }
  },
  mounted() {
    this.consultEmployees();
  },
};
</script>
