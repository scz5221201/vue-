<template>
  <div class="details container">
    <router-link to="/" class="btn btn-default">返回</router-link>
    <h1 class="page-header">
      {{customer.name}}
      <span class="pull-right">
        <router-link v-bind:to="'/edit/'+customer.id" class="btn btn-primary">编辑</router-link>
        <button v-on:click="deleteCustomer(customer.id)" class="btn btn-danger">删除</button>
      </span>
    </h1>

    <ul class="list-group">
      <li class="List-group-item">{{customer.phone}}</li>
      <li class="List-group-item">{{customer.email}}</li>
    </ul>
    <ul class="list-group">
      <li class="List-group-item">{{customer.education}}</li>
      <li class="List-group-item">{{customer.graduationSchool}}</li>
    </ul>
    <ul class="list-group">
      <li class="List-group-item">{{customer.profession}}</li>
      <li class="List-group-item">{{customer.profile}}</li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'customerDetails',
  data() {
    return {
      customer: ""
    }
  },
  methods: {
    fetchCustomers(id) {
      this.$http.get("http://localhost:3000/user/" + id)
        .then(function (response) {
          console.log(response)
          this.customer = response.body;
        })
    },
    deleteCustomer(id) {
      console.log(id)
      this.$http.delete("http://localhost:3000/user/" + id)
        .then(function (response) {
          this.$router.push({ path: "/", query: { alertInfo: "用户信息删除成功" } })
        })
    }
  },
  created() {
    this.fetchCustomers(this.$route.params.id)
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
