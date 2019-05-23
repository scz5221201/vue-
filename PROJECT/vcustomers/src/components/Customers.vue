<template>
  <div class="customers container">
    <div class="page-header">
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
                    <td></td>
                </tr>
            </tbody>
        </table>
    </div>
  </div>
</template>

<script>
export default {
  name: 'customers',
  data () {
    return {
      customers:[]
    }
  },
  methods:{
      fetchCustomers(){
          this.$http.get("http://localhost:3000/user")
          .then(function(response){
              this.customers=response.body;
          })
      }
  },
  created(){
      this.fetchCustomers()
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
