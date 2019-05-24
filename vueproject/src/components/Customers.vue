<template>
  <div class="customers container">
    <div class="page-header">
      <Alert v-if="alertInfo" v-bind:message="alertInfo"></Alert>
      <table class="table table-striped">
        <thead>
          <tr>
            <th>姓名</th>
            <th>电话</th>
            <th>邮箱</th>
            <th></th>
          </tr>
        </thead>

        <tbody>
          <tr v-for="customer in customers">
            <td>{{customer.name}}</td>
            <td>{{customer.phone}}</td>
            <td>{{customer.email}}</td>
            <td>
              <router-link class="btn btn-default" v-bind:to="'/customer/'+customer.id">详情</router-link>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
import Alert from './Alert'
export default {
  name: 'customers',
  data() {
    return {
      customers: [],
      alertInfo: ""
    }
  },
  methods: {
    fetchCustomers() {
      this.$http.get("http://localhost:3000/user")
        .then(function (response) {
          this.customers = response.body;
        })
    },

  },
  created() {
    if (this.$route.query.alertInfo) {
      this.alertInfo = this.$route.query.alertInfo
    }
    this.fetchCustomers()
  },
  updated() {
    this.fetchCustomers()
  },
  components: {
    Alert
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
